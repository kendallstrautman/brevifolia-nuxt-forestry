// this is a dynamically created template

<template>
  <article class="blog">
      <figure class="blog__hero">
          <img :src="post.attributes.hero_image" :alt="post.attributes.title">
      </figure>
    <div class="blog__info" >
      <h1>{{ post.attributes.title }}</h1>
      <h3>{{ formattedDate }}</h3>
    </div>
    <div class="blog__body" v-html="post.html"></div>
    <h2 class="blog__footer">Written By: {{ post.attributes.author }}</h2>
    
  </article>
</template>
<script>
  export default {
    layout: "layout",
    computed: {
      formattedDate() {
        return new Date(this.post.attributes.date).toDateString().slice(4)
      }, 
      nextBlogPath() {
        const firstBlogPath = this.sortedPaths[0]
        const currentPath = this.$nuxt._route.path
        const nextPath = isNull(this.sortedPaths[this.sortedPaths.indexOf(currentPath) + 1]) ? firstBlogPath : this.sortedPaths[this.sortedPaths.indexOf(currentPath) + 1]
        function isNull(item) {
          return item === null || item === undefined
        }
        return nextPath
      } 
    },
    // get the slug as a param to import the correct md file
    async asyncData({ params }) {
      // get this current post, along with all posts(to route next blog)
      try {
        const post = await import(`~/content/blog-posts/${params.slug}.md`);
        const allPosts = await require.context("~/content/blog-posts/", true, /\.md$/)
        const posts =  allPosts.keys().map((key) => {
          return allPosts(key)
        });
        const sortedPosts = posts.sort((a,b) => {
          const dateA = new Date(a.attributes.date);
          const dateB = new Date(b.attributes.date);
          if (dateA < dateB) {
            return 1;
          }
          if (dateA > dateB) {
            return -1;
          }
            return 0;
        })
        const sortedPaths = [] 
        sortedPosts.map(post => {
          const relPath = `/blog${post.attributes._meta.resourcePath.slice(85, -3)}`
          sortedPaths.push(relPath)
        })
        return {
          sortedPaths,
          post,
        }
      } catch(err) {
        return false
      }
    }, 
  }
</script>

// try {
//         const post = await import(`~/content/blog-posts/${params.slug}.md`);
//         return {
//           post
//         }
//       } catch(err) {
//         return false
//       }