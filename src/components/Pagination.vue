<template>
	<div class="pagination-container">
		<div class="pagination-info">
			顯示第 {{ startItem }}-{{ endItem }} 項，共 {{ totalItems }} 項結果
		</div>

		<div class="pagination-controls">
			<button class="pagination-btn prev-btn" :disabled="currentPage === 1"
				@click="$emit('page-change', currentPage - 1)">
				← 上一頁
			</button>

			<div class="page-numbers">
				<button v-for="page in visiblePages" :key="page" class="page-btn"
					:class="{ active: page === currentPage }" @click="$emit('page-change', page)">
					{{ page }}
				</button>
			</div>

			<button class="pagination-btn next-btn" :disabled="currentPage === totalPages"
				@click="$emit('page-change', currentPage + 1)">
				下一頁 →
			</button>
		</div>
	</div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
	currentPage: { type: Number, required: true },
	totalPages: { type: Number, required: true },
	totalItems: { type: Number, required: true },
	itemsPerPage: { type: Number, default: 10 }
})

const emit = defineEmits(['page-change'])

const startItem = computed(() => {
	return (props.currentPage - 1) * props.itemsPerPage + 1
})

const endItem = computed(() => {
	return Math.min(props.currentPage * props.itemsPerPage, props.totalItems)
})

const visiblePages = computed(() => {
	const pages = []
	const maxVisible = 5
	let start = Math.max(1, props.currentPage - Math.floor(maxVisible / 2))
	let end = Math.min(props.totalPages, start + maxVisible - 1)

	if (end - start + 1 < maxVisible) {
		start = Math.max(1, end - maxVisible + 1)
	}

	for (let i = start; i <= end; i++) {
		pages.push(i)
	}

	return pages
})
</script>