<template>
    <q-page>
        <div class="q-pa-lg">
            <div class="row no-wrap shadow-2">
                <q-toolbar class="col" :class="$q.dark.isActive ? 'bg-black text-white' : 'bg-grey-3'">
                    <q-btn flat round dense icon="menu" />
                    <q-toolbar-title></q-toolbar-title>
                    <q-btn flat round dense icon="search" />
                </q-toolbar>
            </div>
        </div>

        <div class="q-pa-xl"></div>

        <div class="flex-center flex">
            <div class="q-pa-xl" style="max-width: 400px">
                <div class="text-bold q-mb-lg text-h4">Log-in</div>
                <div class="q-gutter-mb">
                    <q-input filled v-model="id" label="id" lazy-rules
                        :rules="[val => val && val.length > 0 || 'Please type something']" />

                    <q-input filled type="password" v-model="pwd" label="password" lazy-rules :rules="[
                        val => val !== null && val !== '' || 'Please type your password',
                    ]" />

                    <div class="column q-gutter-y-md">
                        <q-btn @click="Login" label="Login" type="submit" color="black" />
                        <q-btn @click="Signup" label="Signup" type="submit" color="black" to="/signup" />
                    </div>
                </div>
            </div>
        </div>
    </q-page>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const id = ref()
const pwd = ref()
const data = ref({})
const $router = useRouter()

function Login() {
    data.value.id = id.value
    data.value.pw = pwd.value

    if (!id.value || !pwd.value) { //id 또는 pwd가 비어 있으면 경고 메시지 표시
        alert("아이디 또는 비밀번호를 입력하세요")
    }
    else {
        console.log(data.value) //실제 로그인 요청 보내기
        $router.push('/') //로그인 성공 후 index페이지로 이동
    }
}
</script>