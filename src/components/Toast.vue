<template>
  <teleport to="body">
    <transition name="fade">
      <div v-if="visible" class="toast" :class="type">
        {{ message }}
      </div>
    </transition>
  </teleport>
</template>

<script setup>
import { ref } from 'vue'

const visible = ref(false)
const message = ref('')
const type = ref('success')

function showToast(msg, msgType = 'success', duration = 3000) {
  message.value = msg
  type.value = msgType
  visible.value = true
  setTimeout(() => (visible.value = false), duration)
}

defineExpose({ showToast })
</script>

<style scoped>
.toast {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 12px 18px;
  border-radius: 8px;
  color: white;
  font-size: 14px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  opacity: 0.95;
  z-index: 9999;
  transition: all 0.3s ease;
}
.toast.success { background: #4caf50; }
.toast.error { background: #f44336; }
.toast.warning { background: #ff9800; }

.fade-enter-active, .fade-leave-active { transition: opacity 0.3s; }
.fade-enter-from, .fade-leave-to { opacity: 0; }
</style>