<script setup>
import Header from './components/Header.vue'
import posts from './data/data.json'
import PostTable from './components/PostTable.vue'
import DetailModal from './components/DetailModal.vue'
import Pagination from './components/Pagination.vue'
import NewPostModal from './components/NewPostModal.vue'
import Toast from './components/Toast.vue'
import { ref, computed } from 'vue'

const keyword = ref('')
const currentPage = ref(1)
const itemsPerPage = 10
const allPosts = ref([...posts])

const toastRef = ref(null)
function showSuccess() {
	toastRef.value.showToast('資料已成功儲存！', 'success')
}
function showError() {
	toastRef.value.showToast('提交失敗，請稍後再試', 'error')
}

const filteredPosts = computed(() => {
	currentPage.value = 1
	if (!keyword.value) return allPosts.value
	return allPosts.value.filter((p) => {
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

const showShareModal = ref(false)

function openShareModal() {
	showShareModal.value = true
}

function handleNewExperience(newExperience) {
	allPosts.value.unshift(newExperience)
	showShareModal.value = false
	keyword.value = ''
	currentPage.value = 1
}
</script>

<template>
	<Header @share="openShareModal" />
	<main>
		<h2>經驗分享</h2>
		<div class="toast-btns">
			<h2>Toast</h2>
			<button @click="showSuccess">成功</button>
			<button @click="showError">失敗</button>
		</div>
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
		<NewPostModal :visible="showShareModal" @close="showShareModal = false" @submit="handleNewExperience" />
	</main>

	<Toast ref="toastRef" />
</template>

<style>
input[type='search'] {
	padding: 8px;
	width: 100%;
	max-width: 400px;
	margin-bottom: 16px;
	border: 1px solid #ccc;
	border-radius: 4px;
	font-size: 16px;
}

.table-container {
	display: flex;
	justify-content: center;
}

.toast-btns {
	display: flex;
	align-items: center;
	gap: 12px;
	justify-content: center;
	margin-bottom: 1vh;

	& button {
		background: #1a3d64;
		border: none;
		color: white;
		font-size: 1rem;
		padding: 0.5rem 1rem;
		border-radius: 8px;
		cursor: pointer;
		transition: background 0.2s;
	}
}
</style>