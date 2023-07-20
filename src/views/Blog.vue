<script setup>
import axios from 'redaxios'
import { ref } from 'vue';
import { usePostStore } from '../stores/post';

const error = ref('');
const postData = usePostStore()

const perPage = 5


axios.get('api/post')
.then(resp => {
      postData.post = resp.data;
     })
    .catch(err => (error.value = 'Valami hiba történt, próbáld újra!'))
const totalRows = postData.post.length
console.log() //totalRows
</script>

<template>
  <div class="about d-flex flex-column">
    <h1>This is a blog page</h1>
    <h3>{{ totalRows }}</h3>
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
    <nav aria-label="...">
  <ul class="pagination">
    <li class="page-item disabled">
      <span class="page-link">Previous</span>
    </li>
    <li class="page-item"><a class="page-link" href="#">1</a></li>
    <li class="page-item" aria-current="page">
      <span class="page-link">2</span>
    </li>
    <li class="page-item"><a class="page-link" href="#">3</a></li>
    <li class="page-item">
      <a class="page-link" href="#">Next</a>
    </li>
  </ul>
</nav>
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
