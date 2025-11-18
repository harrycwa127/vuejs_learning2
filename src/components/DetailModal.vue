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