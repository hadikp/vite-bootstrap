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
  <div class="about">
    <h1>This is a blog page</h1>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
