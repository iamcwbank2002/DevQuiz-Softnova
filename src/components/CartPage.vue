<template>
  <main class="bg-white p-6 rounded-lg shadow">
    <h2 class="text-2xl font-bold text-gray-800 mb-4">ตะกร้าสินค้า</h2>
    <div v-if="cart.length > 0">
      <ul>
        <li
          v-for="(item, index) in cart"
          :key="index"
          class="flex justify-between items-center border-b py-2"
        >
          <span>{{ item.title }}</span>
          <span>{{ item.price }} บาท</span>
          <button
            class="ml-4 px-2 py-1 bg-red-600 text-white rounded hover:bg-red-700"
            @click="$emit('remove-from-cart', index)"
          >
            ลบ
          </button>
        </li>
      </ul>
      <div class="mt-4 text-right">
        <p class="text-lg font-semibold">ส่วนลด: {{ discount }} บาท</p>
        <p class="text-lg font-semibold">ราคารวมสุทธิ: {{ totalPrice }} บาท</p>
      </div>
    </div>
    <div v-else>
      <p class="text-gray-600">ไม่มีสินค้าในตะกร้า</p>
    </div>
  </main>
</template>

<script>
export default {
  name: "CartPage",
  props: {
    cart: {
      type: Array,
      required: true,
    },
    discount: {
      type: Number,
      required: true,
    },
    totalPrice: {
      type: Number,
      required: true,
    },
  },
};
</script>
