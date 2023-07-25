<script setup>
  import { ref, computed } from 'vue';

  const totalRows = 10
  const perPage = 5
  let page = ref(0)
  let slicePost = []

  const paginate = num => {
  page = num 
  const maxRowThisPage = page * perPage
  slicePost = computed(() => postData.post.slice(maxRowThisPage-perPage,maxRowThisPage))

  const nextPage = () => {
    if (page.value != Math.ceil(postData.post.length / perPage)){
      page.value += 1
    }
  }

  const backPage = () => {
    if (page.value != 1){
      page.value -= 1
    }
  }

  const goToPage = numPage => {
    page.value = numPage
  }
} 

</script>

<template>
  <nav aria-label="Page navigation example">
    <ul class="pagination">
      <li @click="backPage" class="page-item"><a class="page-link" href="#">Previous</a></li>
      <li @click="paginate(1)" class="page-item"><a class="page-link" href="#">1</a></li>
      <li @click="paginate(2)" class="page-item"><a class="page-link" href="#">2</a></li>
      <li @click="paginate(3)" class="page-item"><a class="page-link" href="#">3</a></li>
      <li @click="nextPage" class="page-item"><a class="page-link" href="#">Next</a></li>
    </ul>
</nav>
    <button type="button" class="btn btn-secondary btn-sm ">Small button</button>

</template>

<style scoped>
</style>