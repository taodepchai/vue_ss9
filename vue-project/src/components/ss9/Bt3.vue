<template>
  <div>
    <input type="date" v-model="change" placeholder="Enter some text" />
    
    <p>ngày sinh: {{ change }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const change = ref("");
</script>

<style>
</style>
