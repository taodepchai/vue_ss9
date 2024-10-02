<template>
  <div>
    <h2>Nhân viên</h2>
    <button @click="showAddForm = true">Thêm mới nhân viên</button>

    <input v-model="searchQuery" placeholder="Tìm kiếm theo email" @input="searchEmployee" />

    <table>
      <thead>
        <tr>
          <th>STT</th>
          <th>Họ và tên</th>
          <th>Ngày sinh</th>
          <th>Email</th>
          <th>Địa chỉ</th>
          <th>Trạng thái</th>
          <th>Chức năng</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(employee, index) in filteredEmployees" :key="employee.id">
          <td>{{ index + 1 }}</td>
          <td>{{ employee.name }}</td>
          <td>{{ employee.dob }}</td>
          <td>{{ employee.email }}</td>
          <td>{{ employee.address }}</td>
          <td>
            <span :class="{'active': employee.status, 'inactive': !employee.status}">
              {{ employee.status ? 'Đang hoạt động' : 'Ngừng hoạt động' }}
            </span>
          </td>
          <td>
            <button @click="toggleStatus(index)">{{ employee.status ? 'Chặn' : 'Bỏ chặn' }}</button>
            <button @click="editEmployee(index)">Sửa</button>
            <button @click="deleteEmployee(index)">Xóa</button>
          </td>
        </tr>
      </tbody>
    </table>

    <div v-if="showAddForm || showEditForm">
      <h3>{{ showAddForm ? 'Thêm mới nhân viên' : 'Sửa nhân viên' }}</h3>
      <form @submit.prevent="saveEmployee">
        <input v-model="employeeForm.name" placeholder="Họ và tên" required />
        <input v-model="employeeForm.dob" type="date" placeholder="Ngày sinh" required />
        <input v-model="employeeForm.email" type="email" placeholder="Email" required />
        <input v-model="employeeForm.address" placeholder="Địa chỉ" required />
        <button type="submit">{{ showAddForm ? 'Thêm' : 'Lưu' }}</button>
        <button @click="cancelForm">Hủy</button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const employees = ref([]);
const employeeForm = ref({
  name: '',
  dob: '',
  email: '',
  address: '',
  status: true
});

const showAddForm = ref(false);
const showEditForm = ref(false);
const currentIndex = ref(null);
const searchQuery = ref('');

const loadEmployees = () => {
  const storedEmployees = JSON.parse(localStorage.getItem('employees')) || [];
  employees.value = storedEmployees;
};

const saveEmployees = () => {
  localStorage.setItem('employees', JSON.stringify(employees.value));
};

const saveEmployee = () => {
  if (showAddForm.value) {
    employees.value.push({ ...employeeForm.value, id: Date.now() });
  } else {
    employees.value[currentIndex.value] = { ...employeeForm.value };
  }
  saveEmployees();
  resetForm();
};

const editEmployee = (index) => {
  currentIndex.value = index;
  employeeForm.value = { ...employees.value[index] };
  showEditForm.value = true;
  showAddForm.value = false;
};

const deleteEmployee = (index) => {
  if (confirm('Bạn có chắc chắn muốn xóa?')) {
    employees.value.splice(index, 1);
    saveEmployees();
  }
};

const toggleStatus = (index) => {
  employees.value[index].status = !employees.value[index].status;
  saveEmployees();
};

const filteredEmployees = computed(() => {
  return employees.value.filter((employee) =>
    employee.email.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

const resetForm = () => {
  employeeForm.value = { name: '', dob: '', email: '', address: '', status: true };
  showAddForm.value = false;
  showEditForm.value = false;
  currentIndex.value = null;
};

const cancelForm = () => {
  resetForm();
};

onMounted(() => {
  loadEmployees();
});
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
th, td {
  border: 1px solid #ddd;
  padding: 8px;
}
th {
  background-color: #f2f2f2;
  text-align: left;
}
button {
  margin-right: 5px;
  padding: 5px 10px;
}
.active {
  color: green;
}
.inactive {
  color: red;
}
</style>
