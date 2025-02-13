<template>
  <q-page>
    <div class="q-pa-lg">
      <div class="row no-wrap shadow-2">
        <q-toolbar class="col" :class="$q.dark.isActive ? 'bg-black text-white' : 'bg-grey-3'">
          <q-toolbar-title></q-toolbar-title>
          <q-btn flat round dense icon="search" />
        </q-toolbar>
      </div>
    </div>

    <div class="q-mt-lg flex flex-center text-bold text-h2">Trend Pick</div>
    <div class="q-mt-lg flex flex-center">쇼핑몰 소개 문구</div>

    <div class="q-pa-lg q-mt-lg">
      <q-carousel style="height: 400px" animated v-model="slide" navigation infinite :autoplay="autoplay" arrows
        transition-prev="slide-right" transition-next="slide-left" @mouseenter="autoplay = false"
        @mouseleave="autoplay = true">
        <q-carousel-slide :name="1" img-src="https://cdn.quasar.dev/img/mountains.jpg" />
        <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
        <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
        <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
      </q-carousel>

      <div class="q-mt-xl q-mb-lg flex flex-center text-bold text-h5">{{ category }}</div>

      <div class="row">
        <div class="q-mr-lg q-mb-xl " v-for="(item, i) in items" :key="i" style="width: 340px;">
          <q-card style="max-width: 350px;" class="my-card cursor-pointer" flat bordered>
            <img src="~assets/1.png" @click="Detail(i)">
            <div class="row justify-between items-center q-pa-md">
              <div>
                {{ item }}
                <div class="text-bold">{{ item.name }}</div>
                <div>{{ item.salePrice }}</div>
              </div>
              <q-card-actions align="right">
                <q-btn flat round color="red" icon="favorite" @click="wishlist" />
                <q-btn flat round color="primary" icon="share" />
              </q-card-actions>
            </div>
          </q-card>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { api } from "src/boot/axios";
import { onBeforeMount, onMounted, ref, watch } from "vue";
import { useRoute, useRouter } from "vue-router";
import Cookies from "js-cookie";

const $router = useRouter()
const $route = useRoute()
const slide = ref(1) //첫 번째 슬라이드가 초기 상태에서 표시
const autoplay = ref(true) //캐러셀은 초기 상태에서 자동 재생
const items = ref()
const category = ref($route.query.category || "all"); // 만약 URL에서 category 값을 찾을 수 없으면 all(전체 상품 보기)을 기본값으로 설정)
const token = ref()

// 전체 상품 조회 API
function fetchItems() {
  if (!token.value) return; // 토큰이 없으면 요청하지 않음
  api.get('/item', {
    headers: {
      Authorization: `Bearer ${token.value}`, // JWT 토큰 추가
    },
  })
    .then((res) => {
      console.log(res)
      items.value = res.data.itemData; // API에서 가져온 데이터를 items 배열에 저장
      console.log(items.value);
    })
    .catch((error) => {
      console.error(error);
    })
}

// 카테고리별 상품 조회 API
function fetchCategoryItems(categoryName) {
  // 잘못된 요청 방지
  if (!categoryName || categoryName === "all") {
    fetchItems(); // categoryName이 없거나 all이면 전체 상품을 불러옴
    return;
  }

  api.get(`/item/category/${categoryName}`)
    .then((res) => {
      console.log(res.data);
      items.value = res.data.data; // 데이터 반영
    })
    .catch((error) => {
      console.error(error);
    })
}

// 상품 상세 페이지 이동/조회
function Detail(index) {
  $router.push(`detail?itemId=${index}`)
}

// 위시리스트 상품 추가
function wishlist() {
  api.post(`/wishlist/add`, { itemId: items.value })
    .then((res) => {
      console.log(res.data)
      //$router.push('wishlist')
    })
    .catch((error) => {
      console.error(error)
    });
}

// 페이지 로딩 시 전체 상품 데이터 가져오기
// onMounted: 페이지 처음 로딩시 실행할 코드
onBeforeMount(() => {
  token.value = Cookies.get("jwt_token")
  console.log(Cookies.get("jwt_token")); // 쿠키에 저장된 JWT 확인
})

onMounted(() => {
  fetchCategoryItems(category.value);
});

// 카테고리 변경 감지 및 상품 데이터 다시 불러오기
// Watch: 어떤 값이 바뀌는 것을 감시함
watch(
  () => $route.query.category,
  (newCategory) => {
    console.log("Category changed:", newCategory);
    fetchCategoryItems(newCategory);
  }
);


</script>
