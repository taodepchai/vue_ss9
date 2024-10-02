<template>
  <div>
    <h2>Đăng nhập tài khoản</h2>

    <form @submit.prevent="login">
      <div>
        <label for="email">Email:</label>
        <input type="email" v-model="email" id="email" required />
      </div>

      <div>
        <label for="password">Mật khẩu:</label>
        <input type="password" v-model="password" id="password" required />
      </div>

      <button type="submit">Đăng nhập</button>
    </form>

    <p
      v-if="loginMessage"
      :class="{
        success: loginMessage === 'Đăng nhập thành công',
        error: loginMessage === 'Đăng nhập thất bại',
      }"
    >
      {{ loginMessage }}
    </p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const email = ref("");
const password = ref("");

const login = () => {
  if (!email.value || !password.value) {
    alert("Email và Mật khẩu không được để trống.");
    return;
  }

  const storedUsers = JSON.parse(localStorage.getItem("users")) || [];

  const user = storedUsers.find(
    (user) => user.email === email.value && user.password === password.value
  );

  if (user) {
   alert("Đăng nhập thành công");
  } else {
       alert("Đăng nhập thất bại");

  }
};
</script>

<style scoped></style>
