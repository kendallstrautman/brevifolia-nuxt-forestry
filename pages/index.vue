// the posts are passed down to the Blog List component to be rendered

<template>
  <div>
    <BlogList :posts="posts" />
  </div>
</template>

<script>
import BlogList from '~/components/BlogList.vue'

export default {
  layout: 'layout',
  components: {
    BlogList
  },
  async asyncData() {
      // create context via webpack to map over all blog posts
      const allPosts = await require.context("~/content/blog-posts/", true, /\.md$/)
      const posts =  allPosts.keys().map((key) => {
        // give back the value of each post context
        return allPosts(key)
      });
      return {
        posts
      }
  }
}
</script>