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
    <div class="blog__footer">
      <h2 >Written By: {{ post.attributes.author }}</h2>
      <NuxtLink :to="`/blog/${nextBlogPathMethod()}`">
        <svg xmlns="http://www.w3.org/2000/svg"  version="1.1" x="0px" y="0px" viewBox="0 0 26 26" enableBackground="new 0 0 26 26" >
          <path d="M23.021,12.294l-8.714-8.715l-1.414,1.414l7.007,7.008H2.687v2h17.213l-7.007,7.006l1.414,1.414l8.714-8.713  C23.411,13.317,23.411,12.685,23.021,12.294z"/>
        </svg>
      </NuxtLink>
    </div>
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
        console.log('in computed!')
        console.log(this.sortedPaths)
        console.log(this.currentPath)
        // if there's no 'next' path, return the first path
        const nextPath = isNull(this.sortedPaths[this.sortedPaths.indexOf(this.currentPath) + 1]) ? firstBlogPath : this.sortedPaths[this.sortedPaths.indexOf(this.currentPath) + 1]
        function isNull(item) {
          return item === null || item === undefined
        }
        console.log(this.sortedPaths)
        return nextPath
      } 
    },
    methods: {
      nextBlogPathMethod() {
const firstBlogPath = this.sortedPaths[0]
        console.log('in method!')
        console.log(this.sortedPaths)
        console.log(this.currentPath)
        // if there's no 'next' path, return the first path
        const nextPath = isNull(this.sortedPaths[this.sortedPaths.indexOf(this.currentPath) + 1]) ? firstBlogPath : this.sortedPaths[this.sortedPaths.indexOf(this.currentPath) + 1]
        function isNull(item) {
          return item === null || item === undefined
        }
        console.log(this.sortedPaths)
        return nextPath
      }
    },
    // get the slug as a param to import the correct md file
    async asyncData({ params }) {
      try {
        const currentPath = params.slug
        // get current post data
        const post = await import(`~/content/blog-posts/${params.slug}.md`);
        // get all post data for next route
        const allPosts = await require.context("~/content/blog-posts/", true, /\.md$/)
        const posts =  allPosts.keys().map((key) => {
          return allPosts(key)
        });
        console.log(allPosts.keys())
        console.log(posts)
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
        console.log(sortedPosts)
        const sortedPaths = [] 
        sortedPosts.map(post => {
          console.log(post.attributes._meta.resourcePath)
          // clean up the path
          const relPath = post.attributes._meta.resourcePath.slice(86, -3)
          console.log(relPath)
          sortedPaths.push(relPath)
        })
        console.log(sortedPaths)
        return {
          sortedPaths,
          post,
          currentPath
        }
      } catch(err) {
        console.debug(err)
        return false
      }
    }, 
  }
</script>