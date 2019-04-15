<template>
    <div class="container">
        <article>
            <h1>{{ post.title }}</h1>
            <p>{{ post.body }}</p>
        </article>
    </div>
</template>

<script>

    export default {
        data() {
            return {
                id: this.$route.params.id
            }
        },
        head(){
            return{
                title: this.post.title,
                meta: [
                    { name: 'twitter:title', content: this.post.title},
                    { name: 'twitter:description', content: this.post.content},
                    { name: 'twitter:image', content: 'https://i.imgur.com/UYP2umJ.png'},
                    { name: 'twitter:card', content: 'summary_large_image'}
                ]
            }
        },
        /*async asyncData({params, $axios}) {
            let post = await $axios.$get(`posts/${params.id}`);
            return {post}
        }*/
        computed: {
            post () {
                return this.$store.state.posts.all.find(post => post.id === Number(this.id))
            }
        },
        async fetch ({store, params}) {
            await store.dispatch('posts/fetchPost', params.id)
        }
    }
</script>

<style scoped>
    .container{
        display: flex;
        justify-content: space-between;
        line-height: 1.5;
    }
    article * {
        margin-bottom: 1rem;
    }
    aside{
        min-width: 280px;
        max-width: 280px;
    }
</style>