<template>
  <div class="min-h-screen bg-[#222222] p-6">
    <!-- Navbar -->
    <nav class="bg-white border-gray-200 dark:bg-[#282828]">
      <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
        <!-- Logo -->
        <a href="#" class="flex items-center space-x-3 rtl:space-x-reverse">
          <img src="/public/b9nlogo.png" class="h-20" alt="b9n Logo" @click="goToMainPage" />
          <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white"></span>
        </a>

        <!-- Hamburger Menu Button -->
        <button type="button"
          class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
          @click="toggleMenu" aria-expanded="false">
          <span class="sr-only">Open main menu</span>
          <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M1 1h15M1 7h15M1 13h15" />
          </svg>
        </button>

        <!-- Navbar Menu for Desktop -->
        <div class="hidden md:flex w-full  md:w-auto">
          <ul
            class="font-medium flex flex-col p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 rtl:space-x-reverse md:mt-0 md:border-0 md:bg-white dark:bg-[#282828] dark:border-gray-700">
            <li>
              <a href="#"
                class="block py-2 px-3 text-white bg-[#610094] rounded-sm md:bg-transparent md:text-[#610094] md:p-0 dark:text-white md:dark:text-[#8E05C2] font-bold"
                @click="goToMainPage">หน้าแรก</a>
            </li>
            <li>
              <a href="#"
                class="block py-2 px-3 text-dark:bg-[#282828] rounded-sm hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-[#610094] md:p-0 dark:text-white md:dark:hover:text-[#8E05C2] dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent font-bold"
                @click="goToCartPage">ตะกร้าสินค้า</a>
            </li>




          </ul>
        </div>

        <!-- Mobile Menu (Only when toggled open) -->
        <div v-if="isMenuOpen" class="md:hidden w-full">
          <ul
            class="font-medium flex flex-col p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 dark:bg-[#282828] md:dark:bg-[#282828] dark:border-gray-700">
            <li>
              <a href="#"
                class="block py-2 px-3 text-white bg-[#610094] rounded-sm md:bg-transparent md:text-[#610094] md:p-0 dark:text-white md:dark:text-[#8E05C2] font-bold"
                @click="goToMainPage">หน้าแรก</a>
            </li>
            <li>
              <a href="#"
                class="block py-2 px-3 text-dark:bg-[#282828] rounded-sm hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-[#610094] md:p-0 dark:text-white md:dark:hover:text-[#8E05C2] dark:hover:bg-[#610094] dark:hover:text-white md:dark:hover:bg-transparent font-bold"
                @click="goToCartPage">ตะกร้าสินค้า</a>
            </li>




          </ul>
        </div>
      </div>
    </nav>

    <!-- Content Section -->
    <main v-if="currentPage === 'main'">
      <MainPage :books="books" @add-to-cart="addToCart" />
    </main>
    <main v-else-if="currentPage === 'cart'">
      <CartPage :cart="cart" :discount="discount" :totalPrice="totalPrice" @remove-from-cart="removeFromCart" />
    </main>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import MainPage from "./components/MainPage.vue";
import CartPage from "./components/CartPage.vue";

export default {
  name: "App",
  components: { MainPage, CartPage },
  setup() {
    const books = ref([
      { id: 1, title: "แฮร์รี่ พอตเตอร์กับศิลาอาถรรพ์", price: 100, image: "/public/harry1.jpg" },
      { id: 2, title: "แฮร์รี่ พอตเตอร์กับห้องแห่งความลับ", price: 100, image: "/public/harry2.jpg" },
      { id: 3, title: "แฮร์รี่ พอตเตอร์กับนักโทษแห่งอัซคาบัน", price: 100, image: "/public/harry3.jpg" },
      { id: 4, title: "แฮร์รี่ พอตเตอร์กับถ้วยอัคนี", price: 100, image: "/public/harry4.jpg" },
      { id: 5, title: "แฮร์รี่ พอตเตอร์กับภาคีนกฟีนิกซ์", price: 100, image: "/public/harry5.jpg" },
      { id: 6, title: "แฮร์รี่ พอตเตอร์กับเจ้าชายเลือดผสม", price: 100, image: "/public/harry6.jpg" },
      { id: 7, title: "แฮร์รี่ พอตเตอร์กับเครื่องรางยมทูต", price: 100, image: "/public/harry7.jpg" },
    ]);

    const cart = ref([]);
    const currentPage = ref("main");
    const isMenuOpen = ref(false);

    const addToCart = (book) => {
      cart.value.push(book);
    };

    const removeFromCart = (index) => {
      cart.value.splice(index, 1);
    };

    const goToMainPage = () => {
      currentPage.value = "main";  // เปลี่ยนหน้าเป็นหน้าหลัก
      isMenuOpen.value = false;    // ปิดเมนูมือถือ
    };

    const goToCartPage = () => {
      currentPage.value = "cart";  // เปลี่ยนหน้าเป็นตะกร้าสินค้า
      isMenuOpen.value = false;    // ปิดเมนูมือถือ
    };

    const toggleMenu = () => {
      isMenuOpen.value = !isMenuOpen.value; // Toggle mobile menu
    };

    const discount = computed(() => {
  // ถ้าไม่มีสินค้าในตะกร้า return 0
  if (!cart.value.length) return 0;
  
  // จัดกลุ่มหนังสือตาม id และนับจำนวน
  const bookGroups = cart.value.reduce((acc, item) => {
    acc[item.id] = (acc[item.id] || 0) + 1;
    return acc;
  }, {});
  
  // อัตราส่วนลดตามจำนวนเล่มที่ไม่ซ้ำกัน [0=0%, 1=0%, 2=10%, 3=20%, 4=30%, 5=40%, 6=50%, 7=60%]
  const discountRates = [0, 0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6];
  
  let totalDiscount = 0;
  let tempGroups = { ...bookGroups };
  
  // หาจำนวนชุดที่จะได้ส่วนลดมากที่สุด
  while (Object.values(tempGroups).some(count => count > 0)) {
    // นับจำนวนเล่มที่ไม่ซ้ำกันในรอบนี้
    let uniqueBooksCount = 0;
    
    // ลดจำนวนหนังสือทีละเล่ม
    for (let bookId in tempGroups) {
      if (tempGroups[bookId] > 0) {
        uniqueBooksCount++;
        tempGroups[bookId]--;
      }
    }
    
    // คำนวณส่วนลดสำหรับชุดนี้
    if (uniqueBooksCount > 1) {
      const setPrice = uniqueBooksCount * 100;
      totalDiscount += Math.round(setPrice * discountRates[uniqueBooksCount]);
    }
  }
  
  return totalDiscount;
});

    const totalPrice = computed(() => {
      const total = cart.value.reduce((sum, item) => sum + item.price, 0);
      return total - discount.value;
    });

    return {
      books,
      cart,
      currentPage,
      addToCart,
      removeFromCart,
      isMenuOpen,
      toggleMenu,
      discount,
      totalPrice,
      goToMainPage,
      goToCartPage
    };
  },
};
</script>
