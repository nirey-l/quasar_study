<template>
    <q-page class="flex flex-center">
        <q-card flat style="min-width: 400px;" class="q-pa-md">
            <q-tabs v-model="formType" class="text-grey-7" indicator-color="transparent" active-color="black">
                <q-tab name="user" label="user" />
                <q-tab name="product" label="product" />
            </q-tabs>

            <!-- 사용자 역할 관리 -->
            <div v-if="formType === 'user'" id="user" class="q-gutter-y-lg">
                <q-input v-model="userId" label="사용자 ID" />
                <q-select v-model="userRole" :options="roleOptions" label="역할 변경" />
                <q-btn label="역할 변경" @click="updateUserRole" />>

                사용자 조회
                <div class="q-pa-md">
                    <q-btn label="전체 사용자 조회" @click="fetchUsers" />
                    <q-list v-for="user in users" :key="user.id">
                        <q-item>{{ user.name }} - {{ user.role }}</q-item>
                    </q-list>
                </div>

                사용자 정보 수정
                <div class="q-pa-md">
                    <q-input v-model="selectedUser.name" label="사용자명" />
                    <q-input v-model="selectedUser.email" label="이메일" />
                    <q-btn label="사용자 수정" @click="updateUserInfo" />
                </div>
            </div>

            <div v-else id="product" class="q-gutter-y-lg">
                <!-- 상품 생성 -->
                <div class="q-pa-md">
                    <q-input v-model="newProduct.name" label="상품명" />
                    <q-input v-model="newProduct.price" label="가격" type="number" />
                    <q-input v-model="newProduct.size" label="사이즈" />
                    <q-btn label="상품 생성" @click="createProduct" />
                </div>

                <!-- 상품 조회 -->
                <div class="q-pa-md">
                    <q-input v-model="searchQuery" label="상품명으로 검색" />
                    <q-btn label="상품 조회" @click="searchProduct" />
                </div>

                <!-- 상품 전체 조회 -->
                <div class="q-pa-md">
                    <q-btn label="전체 상품 조회" @click="fetchAllProducts" />
                    <q-list v-for="product in products" :key="product.id">
                        <q-item>{{ product.name }} - {{ product.price }}원</q-item>
                    </q-list>
                </div>

                <!-- 상품 수정 -->
                <div class="q-pa-md">
                    <q-input v-model="selectedProduct.name" label="상품명" />
                    <q-input v-model="selectedProduct.price" label="가격" type="number" />
                    <q-input v-model="selectedProduct.size" label="사이즈" />
                    <q-btn label="상품 수정" @click="updateProduct" />
                </div>

                <!-- 상품 삭제 -->
                <div class="q-pa-md">
                    <q-btn label="상품 삭제" @click="deleteProduct" />
                </div>
            </div>

            <q-btn class="full-width q-mt-md" unelevated square color="primary" no-caps
                @click="formType === 'login' ? login() : register()">
                <q-icon name="login" size="xs"></q-icon>
            </q-btn>

            <q-btn v-if="formType === 'login'" class="full-width q-mt-sm text-weight-light" flat no-caps
                label="forgot password?" @click="findPassword" />

        </q-card>
    </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { api } from 'src/boot/axios'

const users = ref([])
const userId = ref()
const userRole = ref()
const roleOptions = ['Admin', 'User']
const newProduct = ref({
    name: '', description: '', regularPrice: '', sizePrice: '',
    imageUrl: '', size: '', color: '', category: ''
})
// const searchQuery = ref()
const items = ref([
    { id: 1, image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
    { id: 2, image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
    { id: 3, image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
])
const item = items.value // 해당 상품 객체를 가져옴
const itemId = item.id // 해당 상품의 id 값을 가져옴
const selectedProduct = ref({ description: '', size: '' })
const selectedUser = ref({ password: '', name: '' })

// 역할 변경
function updateUserRole() {
    api.post(`/change-role`, { role: userRole.value })
        .then(response => {
            console.log('사용자 역할이 변경되었습니다.', response.data);
        })
        .catch(error => console.error(error))
}

// 상품 생성
function createProduct() {
    api.post(`/create-item`, newProduct.value)
        .then(response => {
            console.log('상품이 생성되었습니다.', response.data);
        })
        .catch(error => console.error(error))
}

// // 상품 조회
// function searchProduct() {
//     api.get(`/item/${itemId}`)
//         .then(response => {
//             items.value = response.data
//         })
//         .catch(error => console.error(error))
// }

// 상품 전체 조회
function fetchAllProducts() {
    api.get(`/items`)
        .then(response => {
            items.value = response.data
        })
        .catch(error => console.error(error))
}

// 상품 정보 수정
function updateProduct() {
    api.patch(`/item/${itemId}`, selectedProduct.value)
        .then(response => {
            console.log('상품이 수정되었습니다.', response.data)
        })
        .catch(error => console.error(error))
}

// 상품 삭제
function deleteProduct() {
    api.delete(`/item/${itemId}`)
        .then(response => {
            console.log('상품이 삭제되었습니다.', response.data)
        })
        .catch(error => console.error(error))
}

// 사용자 조회
function fetchUsers() {
    api.get(`/user/${userId.value}`)
        .then(response => {
            users.value = response.data
        })
        .catch(error => console.error(error))
}

// 사용자 정보 수정
function updateUserInfo() {
    api.put(`/user/${userId.value}`, selectedUser.value)
        .then(response => {
            console.log('사용자 정보가 수정되었습니다.', response.data)
        })
        .catch(error => console.error(error))
}
</script>