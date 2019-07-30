<template>
    <section>
        <ul class="list">
            <li  class="li" >
                <div class="hero_image">
                    <img src="https://source.unsplash.com/random" alt="blog-hero">
                </div>
                <div class="blog__info">
                    <h2>some title</h2>
                    <h3>July 27, 2019</h3>
                
                    <p>
                        Lorem ipsum dolor amet vaporware gochujang iPhone fingerstache 
                        shabby chic slow-carb chambray artisan normcore polaroid sriracha 
                        togen drinking vinegar paleo. Biodiesel cloud bread tote bag
                        yuccie jianbing offal vinyl air plant shaman lomo iceland four loko. 
                        Health goth +1 slow-carb, street art 
                    </p>
                </div>
            </li>
        </ul>
    </section>
</template>
<script>
    export default {
        
        async asyncData() {  
                const resolve = await require.context("~/content/blog-posts/", true, /\.md$/)
                const posts = resolve.keys().map((key) => {
                const  name = key.match(/\/(.+)\.md$/);
                return resolve(name);
            });
            return {
                posts
            }
        },
    }
</script>