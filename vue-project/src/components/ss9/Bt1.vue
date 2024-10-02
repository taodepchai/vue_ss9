<template>
  <div>
    <input type="email" v-model="change" placeholder="" />
    
    <p>email: {{ change }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const change = ref("");
</script>

<style>
</style>
