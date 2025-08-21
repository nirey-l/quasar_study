<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-white text-black q-pa-sm" bordered>
      <q-toolbar>
        <div class="row items-center">
          <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" class="q-mr-lg" />
          <div class="text-h5 text-weight-bold cursor-pointer" @click="Index">
            Trend Pick
          </div>
        </div>

        <q-space />

        <div class="row items-center">
          <q-btn flat round dense icon="login" @click="Login" class="q-ml-sm" />
          <q-btn flat round dense icon="favorite_border" @click="Wishlist" class="q-ml-sm" />
          <q-btn flat round dense icon="shopping_bag" @click="Cart" class="q-ml-sm" />
          <q-btn flat round dense icon="receipt_long" @click="Order" class="q-ml-sm" />
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" bordered>
      <div class="column">
        <q-list>
          <q-expansion-item
            expand-separator
            :label="tab.label"
            default-opened
            v-for="(tab, i) in tabs"
            :key="i"
            auto-close
            stretch
            flat
            header-class="bg-grey-2 text-black"
          >
            <q-item v-for="(option, i) in tab.options" :key="i" clickable @click="Category(option)">
              <q-item-section>{{ option }}</q-item-section>
            </q-item>
          </q-expansion-item>
        </q-list>
      </div>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <div class="bg-white text-black q-pa-lg">

      <q-separator />

      <div class="q-mt-md" style="font-size: 12px; color: #666;">
        <div class="row q-gutter-x-md">
          <span>(주)트렌드픽코리아</span>
          <span>사업자등록번호: 123-45-67890</span>
          <span>대표: 홍길동</span>
          <span>주소: 서울특별시 강남구 테헤란로 123, 45층</span>
        </div>
        <div class="row q-gutter-x-md q-mt-sm">
          <q-btn flat dense no-caps class="text-weight-bold" style="font-size: 12px;" label="개인정보처리방침" />
          <q-btn flat dense no-caps style="font-size: 12px;" label="웹사이트이용약관" />
          <q-btn flat dense no-caps style="font-size: 12px;" label="이용약관" />
        </div>
      </div>
    </div> </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from "vue-router";

const $router = useRouter()
const leftDrawerOpen = ref(false)
const tabs = ref([
  { label:"Best", options: ["TOP", "BOTTOM", "OUTER", "DRESS"] },
])

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

function Login() {
  $router.push('login')
}

function Cart() {
  $router.push('cart')
}

function Index() {
  $router.push('/')
}

function Category(cat) {
  console.log(cat)
  $router.push(`/?category=${cat}`)
}

function Wishlist() {
  console.log()
  $router.push(`wishlist`)
}

function Order() {
  $router.push('order')
}
</script>

<style scoped>
.text-weight-bold {
  font-family: 'Helvetica Neue', sans-serif;
  letter-spacing: 1px;
}
</style>