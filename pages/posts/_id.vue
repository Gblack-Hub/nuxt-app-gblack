<template>
    <div class="container">
        <article>
            <h1 class="title">{{ post.title }}</h1>
            <p>{{ post.content }}</p>
        </article>
        <aside>
            <h3>Posts you ma enjoy</h3>
            <ul>
                <li 
                    v-for="related in relatedPosts"
                >
                    <nuxt-link :to="{name: 'posts-id', params: {id: related.id}}">{{ related.title }}</nuxt-link>
                </li>
            </ul>
        </aside>
    </div>
</template>

<script>
export default {
    head() {
    return {
      title: `Post | ${this.post.title}`,
      meta: [
          { name: 'twitter:title', content: this.post.title },
          { name: 'twitter:description', content: this.post.content },
        //   { name: 'twitter:image', content: this.post.content },
        //   { name: 'twitter:card', content: 'summary_large_image' },
      ]
    }
  },
    computed: {
        post() {
            return this.$store.state.posts.all.find(post => post.id === this.id);
        },
        relatedPosts() {
            return this.$store.state.posts.all.filter(post => post.id !== this.id);
        }
    },
    data() {
        return {
            id: this.$route.params.id,
        }
    }
}
</script>

<style scoped>
    .container {
        display: flex;
        justify-content: space-between;
    }
    article * {
        margin-bottom: 1rem;;
    }
</style>