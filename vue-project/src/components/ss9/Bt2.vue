<template>
  <div>
    <input type="color" v-model="change" placeholder="Enter some text" />
    
    <p>mã màu: {{ change }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const change = ref("");
</script>

<style>
</style>
