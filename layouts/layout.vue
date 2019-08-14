<template>
    <section class="layout">
        <Header :is-info-page="isInfoPage" />
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
        }, 
        computed: {
            isInfoPage() {
                return this.$nuxt._route.name === "info" && true
            }
        }
    }
</script>
