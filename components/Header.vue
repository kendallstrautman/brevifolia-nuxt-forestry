<template>
    <header class="header">
        <nav class="nav">
            <NuxtLink to="/">
                <h1>The Blog Title</h1>
            </NuxtLink>
            <div>
                <h1>
                    <NuxtLink :to="infoRoute">{{ isInfoPage ? "close" : "info" }}</NuxtLink>
                </h1>
            </div>
        </nav>
    </header>
</template>

<script>
    export default {
        props: {
                isInfoPage: {
                    type: Boolean,
                    required: false
            }
        }, 
        computed: {
            infoRoute() {
                return this.isInfoPage ? "/" : "/info"
            }
        }
    }
</script>
