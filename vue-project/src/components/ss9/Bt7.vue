<template>
  <div>
    <h2>Thêm sản phẩm mới</h2>

    <form @submit.prevent="addProduct">
      <div>
        <label for="productCode">Mã sản phẩm:</label>
        <input
          type="text"
          v-model="product.productCode"
          id="productCode"
          required
        />
      </div>

      <div>
        <label for="productName">Tên sản phẩm:</label>
        <input
          type="text"
          v-model="product.productName"
          id="productName"
          required
        />
      </div>

      <div>
        <label for="productPrice">Giá:</label>
        <input
          type="number"
          v-model="product.price"
          id="productPrice"
          required
        />
      </div>

      <div>
        <label for="productQuantity">Số lượng:</label>
        <input
          type="number"
          v-model="product.quantity"
          id="productQuantity"
          required
        />
      </div>

      <button type="submit">Thêm mới</button>
    </form>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const product = reactive({
  productCode: "",
  productName: "",
  price: null,
  quantity: null,
});

const addProduct = () => {
  console.log({
    productCode: product.productCode,
    productName: product.productName,
    price: product.price,
    quantity: product.quantity,
  });
};
</script>

<style scoped></style>
