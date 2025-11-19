<script setup>
import { useCounterStore } from '../stores/counter'
import { storeToRefs } from 'pinia'

const counter = useCounterStore()
const { count } = storeToRefs(counter)
</script>

<template>
  <div>
    <p>現在數字：{{ count }}</p>
    <button @click="counter.increment">增加</button>
    <button @click="counter.reset">重置</button>
  </div>
</template>