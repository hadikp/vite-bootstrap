<script setup>
import axios from 'redaxios'
import { ref, computed } from 'vue';
import { usePostStore } from '../stores/post'

const error = ref('')
const postData = usePostStore()

const totalRows = postData.post.length
const perPage = 2
let page = 0
let slicePost = []

axios.get('api/post')
.then(resp => {
      postData.post = resp.data;
     })
    .catch(err => (error.value = 'Valami hiba történt, próbáld újra!'))

const paginate = num => {
  page = num 
  slicePost = computed(() => postData.post.slice(page,5))
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
    <nav aria-label="Page navigation example">
  <ul class="pagination">
    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
    <li @click="paginate(1)" class="page-item"><a class="page-link" href="#">1</a></li>
    <li @click="paginate(2)" class="page-item"><a class="page-link" href="#">2</a></li>
    <li @click="paginate(3)" class="page-item"><a class="page-link" href="#">3</a></li>
    <li class="page-item"><a class="page-link" href="#">Next</a></li>
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
