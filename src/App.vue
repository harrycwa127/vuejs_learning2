<script setup>
import Header from './components/Header.vue'
import posts from './data/data.json'
import PostTable from './components/PostTable.vue'

</script>

<template>
  <Header />
  <main>
    <h2>經驗分享</h2>
    <PostTable :posts="posts" />
  </main>
</template> 