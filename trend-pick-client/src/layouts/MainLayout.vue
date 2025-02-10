<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="row justify-between bg-black q-py-sm q-px-lg" elevated>
      <div class="row items-center">
        <q-btn class="q-mr-lg" flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />
        <div class="text-h5 class cursor-pointer" @click="Index">
          Trend Pick
        </div>
      </div>

      <div class="row justify-end items-center">
        <q-btn class="q-mr-md" flat round dense icon="login" @click="Login" />
        <q-btn flat round dense icon="shopping_cart" @click="Cart" />
      </div>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <div class="column">
        <q-list>
          <q-expansion-item expand-separator :label="tab.label" default-opened v-for="tab, i in tabs" :key="i" auto-close stretch flat>
            <q-item v-for="option, i in tab.options" :key="i" clickable @click="Category(option)">{{ option }}</q-item>
          </q-expansion-item>
         </q-list> 
      </div>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router';
import { useRouter } from "vue-router";

const $route = useRoute()
const $router = useRouter()
const leftDrawerOpen = ref(false)
const tabs = ref([
  { label:"Best", options: ["아우터", "원피스", "니트", "티셔츠", "블라우스/셔츠", "스커트", "팬츠"] },
  { label: "New", options: ["아우터", "원피스", "니트", "티셔츠", "블라우스/셔츠", "스커트", "팬츠"] }
])
const category = ref()

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

onMounted(() => {
    console.log($route.query.itemId)
    category.value = $route.query.itemId
})
</script>
