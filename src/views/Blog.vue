<script setup>
import axios from 'redaxios'
import { ref, computed } from 'vue';
import { usePostStore } from '../stores/post'

const error = ref('')
const postData = usePostStore()

const totalRows = postData.post.length
const perPage = 5
let page = 0
let slicePost = []

axios.get('api/post')
.then(resp => {
      postData.post = resp.data;
     })
    .catch(err => (error.value = 'Valami hiba történt, próbáld újra!'))

const paginate = num => {
  page = num 
  const maxRowThisPage = page * perPage
  slicePost = computed(() => postData.post.slice(maxRowThisPage-perPage,maxRowThisPage))
} 
  
</script>

<template>
  <div class="about d-flex flex-column">
    <h1>This is a blog page</h1>
    <article v-for="post in slicePost" :key="post.id">
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
