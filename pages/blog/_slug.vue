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
    async asyncData({ params }) {
      try {
        const post = await import(`~/content/blog-posts/${params.slug}.md`);
        return {
          post
        }
      } catch(err) {
        return false
      }
    }, 
    computed: {
      formattedDate() {
        return new Date(this.post.attributes.date).toDateString().slice(4)
      } 
    }
  }
</script>