<template>
  <header class="header">
    <div class="header-content">
      <h1 class="logo">
        ✦ 推甄經驗分享 ✦
      </h1>
      <button class="add-btn" @click="handleShare">
        ✍ 分享經驗
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