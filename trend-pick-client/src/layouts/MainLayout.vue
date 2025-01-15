<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="row justify-between bg-black q-py-sm" elevated>    
        <div class="row items-center">
          <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />
  
          <div class="text-h5">
            Trend Pick
          </div>
        </div>

        <div class="justify-center">
          <q-tabs v-model="tab" class="bg-black text-bold text-white">
            <q-btn-dropdown v-for="tab, i in tabs" :key="i" auto-close stretch flat :label="tab.label">
              <q-list>
                <q-item v-for="option, i in tab.options" :key="i" clickable @click="tab = option">
                  <q-item-section>{{ option }}</q-item-section>
                </q-item>
              </q-list>
            </q-btn-dropdown>
          </q-tabs>
        </div>

        <div class="row justify-end items-center">
          <q-btn flat round dense icon="login" @click="Login" />
          <q-btn flat round dense icon="shopping_cart" @click="Cart"/>
          <q-btn flat round dense icon="favorite" />
        </div>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header>
          Essential Links
        </q-item-label>


      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from "vue-router";

const $router = useRouter()
const leftDrawerOpen = ref(false)
const tab = ref()
const tabs = ref([
  { label: "Best", options: ["아우터", "원피스", "니트", "티셔츠", "블라우스/셔츠", "스커트", "팬츠"] },
  { label: "New", options: ["아우터", "원피스", "니트", "티셔츠", "블라우스/셔츠", "스커트", "팬츠"] }
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
</script>
