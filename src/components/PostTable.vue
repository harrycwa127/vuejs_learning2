<template>
    <table class="post-table">
        <thead>
            <tr>
                <th>學校</th>
                <th>系所</th>
                <th>年度</th>
                <th>日期</th>
                <th>Score</th>
                <th>結果</th>
                <th>來源</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="post in posts" :key="post.pId">
                <td>{{ post.pSchool }}</td>
                <td>{{ post.pDep }}</td>
                <td>{{ post.pYear }}</td>
                <td>{{ post.pDate }}</td>
                <td>{{ post.pScore ?? '-' }}</td>
                <td>{{ post.pResult1 }}</td>
                <td>
                    <a v-if="post.pURL" :href="post.pURL" target="_blank">來源</a>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script setup>
    const props = defineProps({
        posts: { type: Array, default: () => [] }
    })
</script>