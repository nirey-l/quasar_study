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

        <div class="q-pa-xl"></div>

        <div class="flex-center flex">
            <div class="q-pa-xl" style="max-width: 900px">
                <div class="text-bold q-mb-lg text-h4">Log-in</div>
                <div class="q-gutter-mb">
                    <q-input filled v-model="id" label="id" lazy-rules
                        :rules="[val => val && val.length > 0 || 'Please type something']" />

                    <q-input filled type="password" v-model="pwd" label="password" lazy-rules :rules="[
                        val => val !== null && val !== '' || 'Please type your password',
                    ]" />

                    <div class="row justify-between">
                        <q-btn @click="Login" label="Login" type="submit" color="black" />
                        <q-btn @click="Signup" label="Signup" type="submit" color="black" to="/signup" />
                    </div>

                    <div class="flex-center flex q-my-md ">
                        <q-btn flat @click="find_pwd" label="forgot pwd?" type="submit" to="/find_pwd"/>
                    </div>
                </div>
            </div>
        </div>
    </q-page>
</template>

<script setup>
import { api } from "src/boot/axios";
import { ref } from "vue";
import { useRouter } from "vue-router";

const id = ref()
const pwd = ref()
const $router = useRouter()


function Login() {
    if (!id.value || !pwd.value) { //id 또는 pwd가 비어 있으면 경고 메시지 표시
        alert("아이디 또는 비밀번호를 입력하세요")
    }
    else {
        api.post('/auth/login', { email: id.value, password: pwd.value })
            .then((res) => {
                console.log(res.data);
                if (res.data.message === "로그인 성공") {
                    //  r.data.userData.jwtToken  

                    $router.push('/') //로그인 성공 후 index페이지로 이동
                } else {
                    alert('로그인 실패')
                }
            })
            .catch((error) => {
                console.error(error);
                alert('로그인 실패')
            });
    }
}
</script>