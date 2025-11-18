<script setup>
import Header from './components/Header.vue'
import posts from './data/data.json'
import PostTable from './components/PostTable.vue'
import DetailModal from './components/DetailModal.vue'
import Pagination from './components/Pagination.vue'
import { ref, computed } from 'vue'

const keyword = ref('')
const currentPage = ref(1)
const itemsPerPage = 10

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

function handlePageChange(page) {
	currentPage.value = page
	// Scroll to top when page changes
	window.scrollTo({ top: 0, behavior: 'smooth' })
}
const totalPages = computed(() => {
	return Math.ceil(filteredPosts.value.length / itemsPerPage)
})

const paginatedPosts = computed(() => {
	const start = (currentPage.value - 1) * itemsPerPage
	const end = start + itemsPerPage
	return filteredPosts.value.slice(start, end)
})
</script>

<template>
	<Header />
	<main>
		<h2>經驗分享</h2>
		<input v-model="keyword" type="search" placeholder="請輸入原學校、系所或欲推甄校系" class="search-box" />
		<div v-if="filteredPosts.length > 0">
			<div class="table-container">
				<PostTable :posts="paginatedPosts" @select="openDetail" />
			</div>

			<Pagination v-if="totalPages > 1" :current-page="currentPage" :total-pages="totalPages"
				:total-items="filteredPosts.length" :items-per-page="itemsPerPage" @page-change="handlePageChange" />
		</div>
		<p v-else>查無相關結果 QQ</p>
		<DetailModal :visible="showModal" :post="selectedPost" @close="showModal = false" />
	</main>
</template>