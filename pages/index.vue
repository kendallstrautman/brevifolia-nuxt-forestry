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
      const allPosts = await require.context("~/content/blog-posts/", true, /\.md$/)
      const posts =  allPosts.keys().map((key) => {
        return allPosts(key)
      });
      return {
        posts
      }
  }
}
</script>

  // const resolve = await require.context("~/content/blog-posts/", true, /\.md$/)
  //     const imports = resolve.keys().map((key) => {
  //       const  name = key.match(/\/(.+)\.md$/);
  //       return resolve(name);
  //     });
  //     return {
  //       posts: imports
  //     }
