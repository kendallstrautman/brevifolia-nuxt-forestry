<template>
    <section>
        <ul class="list">
            <NuxtLink  
                v-for="post in sortedPosts" 
                :key="post.attributes.title" 
                :to="`/blog/${formatSlug(post.attributes.title)}`"
            >
                <li>
                    <div class="hero_image">
                        <img :src="post.attributes.hero_image" :alt="post.attributes.title">
                    </div>
                    <div class="blogList__info">
                        <h2>{{ post.attributes.title }}</h2>
                        <h3>{{ formatDate(post.attributes.date) }}</h3>
                        <p>{{ formatExcerpt(post.body) }}...</p>
                    </div>
                </li>
            </NuxtLink>                  
        </ul>
    </section>                       
</template>
<script>
    export default {
        props: ['posts'], 
        computed: {
            sortedPosts() {
                const sortedPosts = this.posts
                sortedPosts.sort((a,b) => {
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
                return sortedPosts
            }
        },
        methods: {
            formatDate(date) {
                return new Date(date).toDateString().slice(4)
            }, 
            formatExcerpt(body) {
                return body.slice(0 , 200).trimEnd()
            }, 
            formatSlug(title) {
                const regex = / /gi;
                return title.toLowerCase().trim().replace(regex, "-")
            }
        }
    }
</script>

/* 

#2 - i would love to figure out how to show the md in the summary... right now its just plaintext
 */



