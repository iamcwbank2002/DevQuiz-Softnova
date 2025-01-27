<template>
  <div class="bg-[#282828] rounded-md shadow-lg">
    <!-- Hero Section -->
    <div class="relative isolate px-6 pt-14 lg:px-8 m-6">
      <!-- Background Gradient -->
      <div
        class="absolute inset-x-0 -top-40 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80"
        aria-hidden="true"
      >
        <div
          class="relative left-[calc(50%-11rem)] aspect-1155/678 w-[36.125rem] -translate-x-1/2 rotate-[30deg] bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%-30rem)] sm:w-[72.1875rem]"
          style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
        ></div>
      </div>
      <div class="mx-auto max-w-2xl py-32 sm:py-48 lg:py-56">
        <div class="hidden sm:mb-8 sm:flex sm:justify-center"></div>
        <div class="text-center">
          <!-- Main Heading -->
          <h1 class="text-4xl sm:text-5xl font-bold tracking-tight text-white text-shadow-md mb-6">
            BAN9DIN Shop ตอนนี้เรามีโปรโมชั่น!!
          </h1>
          <!-- Sub Headings with Promotion Details -->
          <h3 class="text-xl sm:text-2xl font-semibold tracking-tight text-white">
            ซื้อไม่ซ้ำกัน 2 เล่ม ลด 10% ของ 2 เล่มนั้น
          </h3>
          <h3 class="text-xl sm:text-2xl font-semibold tracking-tight text-white">
            ซื้อไม่ซ้ำกัน 3 เล่ม ลด 20% ของ 3 เล่มนั้น
          </h3>
          <h3 class="text-xl sm:text-2xl font-semibold tracking-tight text-white">
            ซื้อไม่ซ้ำกัน 4 เล่ม ลด 30% ของ 4 เล่มนั้น
          </h3>
          <h3 class="text-xl sm:text-2xl font-semibold tracking-tight text-white">
            ซื้อไม่ซ้ำกัน 5 เล่ม ลด 40% ของ 5 เล่มนั้น
          </h3>
          <h3 class="text-xl sm:text-2xl font-semibold tracking-tight text-white">
            ซื้อไม่ซ้ำกัน 6 เล่ม ลด 50% ของ 6 เล่มนั้น
          </h3>
          <h3 class="text-xl sm:text-2xl font-semibold tracking-tight text-white">
            ซื้อไม่ซ้ำกัน 7 เล่ม ลด 60% ของ 7 เล่มนั้น
          </h3>
          <p class="mt-8 text-lg font-medium text-pretty text-gray-500 sm:text-xl">
            BAN9DINShop
          </p>
        </div>
      </div>
      <!-- Background Gradient Overlay -->
      <div
        class="absolute inset-x-0 top-[calc(100%-13rem)] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[calc(100%-30rem)]"
        aria-hidden="true"
      >
        <div
          class="relative left-[calc(50%+3rem)] aspect-1155/678 w-[36.125rem] -translate-x-1/2 bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%+36rem)] sm:w-[72.1875rem]"
          style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
        ></div>
      </div>
    </div>

    <!-- Book Cards Section (Responsive Grid) -->
    <main class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-3">
      <BookCard
        v-for="book in books"
        :key="book.id"
        :book="book"
        @add-to-cart="addToCart"
      />
    </main>
  </div>
</template>

<script>
import BookCard from "./BookCard.vue";

export default {
  name: "MainPage",
  components: { BookCard },
  props: {
    books: {
      type: Array,
      required: true,
    },
  },
  emits: ["add-to-cart"],
  methods: {
    addToCart(book) {
      this.$emit("add-to-cart", book);
    },
  },
};
</script>

  