<template>
    <div v-if="visible" class="modal-overlay">
        <div class="modal-content">
            <div class="modal-header">
                <h3>{{ post?.pSchool }} {{ post?.pDep }}</h3>
                <button class="close" @click="close">×</button>
            </div>
            <section class="content">
                <p><strong>年度：</strong>{{ post?.pYear }}</p>
                <p><strong>日期：</strong>{{ post?.pDate }}</p>
    
                <h4>背景 / 經歷</h4>
                <pre>{{ post?.pExp || '無' }}</pre>
    
                <h4>結果</h4>
                <pre>{{ post?.pResult1 || '無' }}</pre>
    
                <h4>來源</h4>
                <a v-if="post?.pURL" :href="post.pURL" target="_blank">查看 Dcard 原文</a>
            </section>
        </div>
    </div>
</template>

<script setup>
    const props = defineProps({
        post: { type: Object, default: null },
        visible: { type: Boolean, default: false }
    });

    const emit = defineEmits(['close']);;
    function close() {
        emit('close');
    };
</script>

<style>
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;
    box-sizing: border-box;
    z-index: 1000;
}

.modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    width: 90%;
    max-width: 600px;
    max-height: 80%;
    overflow-y: auto;
    position: relative;
}

.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>