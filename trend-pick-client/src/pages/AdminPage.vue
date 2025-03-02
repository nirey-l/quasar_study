<template>
    <q-page class="flex flex-center">
        <q-card flat style="min-width: 400px;" class="q-pa-md">
            <q-tabs v-model="formType" class="text-grey-7" indicator-color="transparent" active-color="black">
                <q-tab name="user" label="User" />
                <q-tab name="product" label="Product" />
            </q-tabs>

            <!-- 사용자 관리 -->
            <q-card-section v-if="formType === 'user'">
                <q-input v-model="userId" label="사용자 ID" />
                <q-select v-model="userRole" :options="roleOptions" label="역할 변경" />
                <q-btn label="역할 변경" @click="updateUserRole" class="q-mr-md" />

                <q-btn label="전체 사용자 조회" @click="fetchUsers" />
                <q-list>
                    <q-item v-for="user in users" :key="user.id">
                        {{ user.name }} - {{ user.role }}
                    </q-item>
                </q-list>

                <q-input v-model="selectedUser.name" label="사용자명" />
                <q-input v-model="selectedUser.email" label="이메일" />
                <q-btn label="사용자 수정" @click="updateUserInfo" />
            </q-card-section>

            <!-- 상품 관리 -->
            <q-card-section v-else>
                <q-input v-model="newProduct.name" label="상품명" />
                <q-input v-model="newProduct.price" label="가격" type="number" />
                <q-input v-model="newProduct.size" label="사이즈" />
                <q-btn label="상품 생성" @click="createProduct" />

                <q-input v-model="searchQuery" label="상품명으로 검색" />
                <q-btn label="상품 조회" @click="searchProduct" />
                
                <q-btn label="전체 상품 조회" @click="fetchAllProducts" class="q-ml-md" />
                <q-list>
                    <q-item v-for="product in products" :key="product.id">
                        {{ product.name }} - {{ product.price }}원
                    </q-item>
                </q-list>

                <q-input v-model="selectedProduct.name" label="상품명" />
                <q-input v-model="selectedProduct.price" label="가격" type="number" />
                <q-input v-model="selectedProduct.size" label="사이즈" />
                <q-btn label="상품 수정" @click="updateProduct" />
                <q-btn label="상품 삭제" @click="deleteProduct" class="q-ml-md" />
            </q-card-section>
        </q-card>
    </q-page>
</template>

<script setup>
import { ref } from 'vue';
import { api } from 'src/boot/axios';

const formType = ref('user');
const users = ref([]);
const userId = ref('');
const userRole = ref('');
const roleOptions = ['Admin', 'User'];
const newProduct = ref({ name: '', price: '', size: '' });
const searchQuery = ref('');
const products = ref([]);
const selectedUser = ref({ id: null, name: '', email: '' });
const selectedProduct = ref({ id: null, name: '', price: '', size: '' });

// 사용자 역할 변경
function updateUserRole() {
    api.post(`/change-role/${userId.value}`, { role: userRole.value })
        .then(response => console.log('사용자 역할이 변경되었습니다.', response.data))
        .catch(error => console.error(error));
}

// 전체 사용자 조회
function fetchUsers() {
    api.get(`/users`)
        .then(response => users.value = response.data)
        .catch(error => console.error(error));
}

// 사용자 정보 수정
function updateUserInfo() {
    api.put(`/user/${selectedUser.value.id}`, selectedUser.value)
        .then(response => console.log('사용자 정보가 수정되었습니다.', response.data))
        .catch(error => console.error(error));
}

// 상품 생성
function createProduct() {
    api.post(`/create-item`, newProduct.value)
        .then(response => console.log('상품이 생성되었습니다.', response.data))
        .catch(error => console.error(error));
}

// 상품 검색
function searchProduct() {
    api.get(`/items`, { params: { query: searchQuery.value } })
        .then(response => products.value = response.data)
        .catch(error => console.error(error));
}

// 전체 상품 조회
function fetchAllProducts() {
    api.get(`/items`)
        .then(response => products.value = response.data)
        .catch(error => console.error(error));
}

// 상품 수정
function updateProduct() {
    api.patch(`/item/${selectedProduct.value.id}`, selectedProduct.value)
        .then(response => console.log('상품이 수정되었습니다.', response.data))
        .catch(error => console.error(error));
}

// 상품 삭제
function deleteProduct() {
    api.delete(`/item/${selectedProduct.value.id}`)
        .then(response => console.log('상품이 삭제되었습니다.', response.data))
        .catch(error => console.error(error));
}
</script>
