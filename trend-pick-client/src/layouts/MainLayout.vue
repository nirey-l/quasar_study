<template>
  <q-layout view="lHh Lpr lFf">
    <q-header 
      class="bg-white text-black" 
      bordered 
      @mouseleave="isSubNavVisible = false"
    >
      <q-toolbar class="q-px-xl q-py-md">
        <div 
          class="row items-center q-gutter-x-md" 
          @mouseover="showSubNav('Trend')"
        >
          <q-btn flat no-caps dense label="Trend" class="text-subtitle1 text-weight-bold" />
        </div>
        <div 
          class="row items-center q-gutter-x-md q-ml-sm"
          @mouseover="showSubNav('Pick')"
        >
          <q-btn flat no-caps dense label="Pick" class="text-subtitle1 text-weight-bold" />
        </div>

        <q-space />
        <div class="text-h3 text-weight-bold cursor-pointer main-logo" @click="Index">
          Trend Pick
        </div>
        <q-space />

        <div class="row items-center q-gutter-x-md">
          <q-btn flat dense round icon="search" />
          <q-btn flat round dense icon="person_outline" @click="Login" />
          <q-btn flat round dense icon="favorite_border" @click="Wishlist" />
          <q-btn flat round dense icon="shopping_bag" @click="Cart" />
        </div>
      </q-toolbar>

      <q-toolbar v-show="isSubNavVisible" class="q-px-xl q-py-sm transition-show">
        <q-btn
          v-for="nav in activeSubNav"
          :key="nav"
          flat
          dense
          no-caps
          :label="nav"
          class="text-subtitle2 text-weight-medium q-mr-lg"
          @click="goTo(nav)"
        />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <div class="q-pa-xl bg-white text-black footer-container">
      <div class="row justify-between items-center">
        <div class="row q-gutter-x-md">
          <q-btn flat dense no-caps label="(주)트렌드픽" class="footer-link text-weight-bold" />
          <q-btn flat dense no-caps label="이용약관" class="footer-link" />
          <q-btn flat dense no-caps label="개인정보처리방침" class="footer-link" />
          <q-btn flat dense no-caps label="이용안내" class="footer-link" />
          <q-btn flat dense no-caps label="고객센터" class="footer-link" />
        </div>
        <div>
          <q-btn flat dense icon="fab fa-instagram" />
        </div>
      </div>

      <q-separator class="q-my-lg" />

      <div class="text-caption text-grey-7 footer-info">
        <p>
          대표. 홍길동 | 대표전화. 1234-5678 | 주소. 서울특별시 강남구 테헤란로 123, 45층<br>
          사업자등록번호. 123-45-67890 [사업자정보확인]<br>
          통신판매업신고. 2025-서울강남-01234
        </p>
        <p>© TrendPick All rights reserved.</p>
      </div>
    </div>

  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from "vue-router";

const $router = useRouter();

const isSubNavVisible = ref(false);

const subNavs = {
  Trend: ['New in', 'Project', 'Collection', 'Shop', 'Archive', 'About'],
  Pick: ['Outwears', 'Tops', 'Bottoms', 'Dresses', 'Bags', 'Shoes']
};

const activeSubNav = ref([]);

function showSubNav(menuType) {
  isSubNavVisible.value = true;
  activeSubNav.value = subNavs[menuType];
}

function goTo(pageName) {
  const path = pageName.toLowerCase().replace(' ', '-');
  $router.push(`/${path}`);
}

function Login() { $router.push('login') }
function Cart() { $router.push('cart') }
function Index() { $router.push('/') }
function Wishlist() { $router.push('wishlist') }
</script>

<style scoped>
.text-weight-bold {
  font-family: 'Helvetica Neue', sans-serif;
  letter-spacing: 1px;
}

/* 👇 New style for the main logo */
.main-logo {
  font-family: 'Times New Roman', Times, serif; /* Font from 'Modern Classic' */
}

.transition-show {
  transition: opacity 0.3s ease, transform 0.3s ease;
  transform-origin: top;
}
.q-header .q-toolbar[style*="display: none"] {
  opacity: 0;
  transform: translateY(-10px);
}

/* Footer styles */
.footer-container {
  border-top: 1px solid #e0e0e0;
}
.footer-link {
  padding: 0 4px;
}
.footer-info p {
  margin: 0 0 8px 0;
}
</style>
