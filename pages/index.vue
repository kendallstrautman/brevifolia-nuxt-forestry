<template>
  <div>
    <BlogList />
  </div>
</template>

<script>
import BlogList from '~/components/BlogList.vue'

export default {
  layout: 'layout',
  components: {
    BlogList
  }
}
</script>
