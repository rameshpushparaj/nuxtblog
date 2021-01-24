<template>
  <div class="container">
    <p v-if="$fetchState.pending">Fetching posts...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
  <div v-else>
    <h1 class="page-heading">Nuxt Blog Posts</h1>
    <ul>
      <li v-for="post of posts" :key="post.id">
         <h3 class="title"> {{ post.title }} </h3>
         <p class="postbody"> {{ post.body }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
    data() {
      return {
        posts: []
      }
    },
    async fetch() {
      this.posts = await fetch(
        'http://jsonplaceholder.typicode.com/posts?_start=0&_limit=10'
      ).then(res => res.json())
    }
  }
</script>


<style>

.title {
    text-transform: capitalize;
    color: #526488;
}
.postbody {
    padding: 20px;
}

</style>
