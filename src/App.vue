<script setup>
import Header from './components/Header.vue'
import posts from './data/data.json'
import PostTable from './components/PostTable.vue'
import DetailModal from './components/DetailModal.vue'
import { ref, computed } from 'vue'

const keyword = ref('')

const filteredPosts = computed(() => {
	if (!keyword.value) return posts
	return posts.filter((p) => {
		return (
			p.pSchool?.includes(keyword.value) ||
			p.pDep?.includes(keyword.value) ||
			p.pResult1?.includes(keyword.value)
		)
	})
});

const selectedPost = ref(null)
const showModal = ref(false)

function openDetail(post) {
	selectedPost.value = post
	showModal.value = true
}
</script>

<template>
	<Header />
	<main>
		<h2>經驗分享</h2>
		<input v-model="keyword" type="search" placeholder="請輸入原學校、系所或欲推甄校系" class="search-box" />
		<PostTable :posts="filteredPosts" v-if="filteredPosts.length > 0" @select="openDetail" />
		<p v-else>查無相關結果 QQ</p>
		<DetailModal :visible="showModal" :post="selectedPost" @close="showModal = false" />
	</main>
</template>