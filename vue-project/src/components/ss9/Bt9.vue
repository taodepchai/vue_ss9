<template>
  <div>
    <h2>Đăng ký tài khoản</h2>

    <form @submit.prevent="register">
      <div>
        <label for="studentName">Tên sinh viên:</label>
        <input
          type="text"
          v-model="user.name"
          id="studentName"
          ref="studentNameInput"
          required
        />
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
        <label for="address">Địa chỉ:</label>
        <input type="text" v-model="user.address" id="address" />
      </div>

      <button type="submit">Đăng ký</button>
    </form>

    <p v-if="successMessage" class="success">{{ successMessage }}</p>
  </div>
</template>

<script setup>
import { reactive, ref, onMounted } from "vue";

const user = reactive({
  name: "",
  email: "",
  password: "",
  address: "",
});

const studentNameInput = ref(null);

const focusOnStudentName = () => {
  studentNameInput.value.focus();
};

const isEmailDuplicate = (email) => {
  const storedUsers = JSON.parse(localStorage.getItem("users")) || [];
  return storedUsers.some((user) => user.email === email);
};

const register = () => {
  if (!user.name || !user.email || !user.password) {
    alert("Tên sinh viên, Email và Mật khẩu không được để trống.");
    return;
  }

  if (isEmailDuplicate(user.email)) {
    alert("Email đã tồn tại. Vui lòng sử dụng email khác.");
    return;
  }

  const newUser = { ...user };
  const storedUsers = JSON.parse(localStorage.getItem("users")) || [];
  storedUsers.push(newUser);
  localStorage.setItem("users", JSON.stringify(storedUsers));


  user.name = "";
  user.email = "";
  user.password = "";
  user.address = "";

  focusOnStudentName();
};

onMounted(() => {
  focusOnStudentName();
});
</script>

<style scoped>

</style>
