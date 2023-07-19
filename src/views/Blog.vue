<script setup>
import axios from 'redaxios'
import { ref } from 'vue';
import { usePostStore } from '../stores/post';

const error = ref('');
const postData = usePostStore()

axios.get('api/post')
.then(resp => {
      postData.post = resp.data;
     })
    .catch(err => (error.value = 'Valami hiba történt, próbáld újra!'))
</script>

<template>
  <div class="about d-flex flex-column">
    <h1>This is a blog page</h1>
    <article v-for="post in postData.post" :key="post.id">
      <div class="article-date">
        <!-- <h3> Published on: {{ date(post.createdAt).format('YYYY-MM-DD HH:mm') }} </h3> -->
      
      <div class="article-head">
        <h3>{{ post.title }}</h3>
      </div>
      <div class="article-body">
        <!-- <img width="50" height="30" src="" alt="" /> -->
        <p> {{ post.content }} </p>
      </div>
    </div>
    </article>
    <button type="button" class="btn btn-secondary btn-sm ">Small button</button>

  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    margin: 1rem;
    /* min-height: 100vh;
    display: flex;
    align-items: center; */
  }
}
</style>
