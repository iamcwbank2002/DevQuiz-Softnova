<template>
  <div class="m-4 p-6 bg-gradient-to-r from-[#8E05C2] to-[#3E065F] rounded-lg shadow-lg hover:shadow-xl transition-transform transform hover:scale-105">
    <img :src="book.image" :alt="book.title" class="w-32 h-32 sm:w-40 sm:h-40 object-cover mb-4 rounded-lg border-4 border-white shadow-md" />
    <h2 class="text-xl sm:text-2xl font-bold text-white">{{ book.title }}</h2>
    <p class="mt-2 text-gray-200 text-sm sm:text-lg">ราคา: {{ book.price }} บาท</p>
    <button 
      class="mt-4 px-4 py-2 sm:px-6 sm:py-2 bg-[#7700ff] text-white rounded-lg shadow-md hover:bg-red-500 transition duration-200 active:scale-95"
      @click="$emit('add-to-cart', book)"
    >
      เพิ่มลงตะกร้า
    </button>
  </div>
</template>

<script>
export default {
  name: "BookCard",
  props: {
    book: {
      type: Object,
      required: true,
    },
  },
};
</script>

