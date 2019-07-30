<template>
    <section>
        <ul class="list">
            <NuxtLink>
                <li v-for="post in posts" :key="post.attributes.title" >
                    <div class="hero_image">
                        <img :src="post.attributes.hero_image" :alt="post.attributes.title">
                    </div>
                    <div class="blog__info">
                        <h2>{{ post.attributes.title }}</h2>
                        <h3>{{ post.attributes.date }}</h3>
                        <p>{{post.body.slice(0 , 200).trimEnd()}}...</p>
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
            generateSlugs() {
                // try to map the slugs to data somehow and v-for over those with the nuxt link???? is is possible 
                //  to compute properties with props instead of data?????? is the question
                // let slugs = []
                // posts.map(post => slugs.push(post.attributes.title))
                return null
            }
        }
    }
</script>


// <div class="hero_image">
//                     <img src="https://source.unsplash.com/random" alt="blog-hero">
//                 </div>
//                 <div class="blog__info">
//                     <h2>some title</h2>
//                     <h3>July 27, 2019</h3>
                    
//                     <p>
//                         Lorem ipsum dolor amet vaporware gochujang iPhone fingerstache 
//                         shabby chic slow-carb chambray artisan normcore polaroid sriracha 
//                         togen drinking vinegar paleo. Biodiesel cloud bread tote bag
//                         yuccie jianbing offal vinyl air plant shaman lomo iceland four loko. 
//                         Health goth +1 slow-carb, street art 
//                     </p>
//                 </div>