<template>
  <div>
    <p>giới tính {{gender }}</p>
    <input type="radio" v-model="gender" name="" id="male" value="nam" />
    <label for="male">nam</label>
    <input type="radio" v-model="gender" name="" id="female" value="nữ" />
    <label for="female">nữ</label>
    <input type="radio" v-model="gender" name="" id="diff" value="khác" />
    <label for="diff">khác</label>
  </div>
</template>

<script setup> 
    import { ref } from 'vue';
    const gender = ref('nam');
</script>

<style></style>
