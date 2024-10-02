<template>
  <div>
    <h2>Đăng ký tài khoản</h2>
    
    <form @submit.prevent="register">
      <div>
        <label for="name">Tên:</label>
        <input type="text" v-model="user.name" id="name" required />
      </div>

      <div>
        <label for="email">Email:</label>
        <input type="email" v-model="user.email" id="email" required />
      </div>

      <div>
        <label for="password">Mật khẩu:</label>
        <input type="password" v-model="user.password" id="password" required />
      </div>

      <div>
        <label for="confirmPassword">Nhập lại mật khẩu:</label>
        <input type="password" v-model="user.confirmPassword" id="confirmPassword" required />
      </div>

      <button type="submit">Đăng ký</button>
    </form>
  </div>
</template>

<script setup>
import { reactive } from 'vue';

const user = reactive({
  name: "",
  email: "",
  password: "",
  confirmPassword: ""
});

const register = () => {
  console.log({
    name: user.name,
    email: user.email,
    password: user.password,
    confirmPassword: user.confirmPassword
  });
};
</script>

<style scoped>

</style>
