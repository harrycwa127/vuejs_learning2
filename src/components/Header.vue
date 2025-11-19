<template>
	<header class="header">
		<div class="header-content">
			<h1 class="logo">
				<router-link to="/" class="logo-link">
					✦ Vue.js 自學 ✦
				</router-link>
			</h1>
			<nav class="nav-menu">
				<router-link to="/" class="nav-link">首頁</router-link>
				<router-link to="/about" class="nav-link">關於</router-link>
			</nav>
			<button class="add-btn" @click="handleShare">
				✍ 新增
			</button>
		</div>
	</header>
</template>


<script setup>
const emit = defineEmits(['share'])

function handleShare() {
	emit('share')
}
</script>

<style scoped>
a {
	color: white;
	text-decoration: none;
	margin-right: 20px;
}
</style>