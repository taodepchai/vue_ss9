<template>
  <div>
    <input type="range" v-model="change" placeholder="Enter some text" />
    
    <p>tiến độ hoàn thành: {{ change }} %</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const change = ref("");
</script>

<style>
</style>
