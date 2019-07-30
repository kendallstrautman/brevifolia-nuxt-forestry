<template>
    <section class="layout">
        <Header />
        <div class="content">
            <nuxt />
        </div>
    </section>
</template>

<script>
import Header from '~/components/Header.vue'

    export default {
        components: {
            Header
        }
    }
</script>
