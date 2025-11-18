<template>
  <header class="header">
    <div class="header-content">
      <h1 class="logo">
        ✦ Vue.js 自學 ✦
      </h1>
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