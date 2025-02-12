<template>
    <div class="q-pa-xl"></div>
    <div class="flex flex-center q-pa-xl">
        <div class="q-pa-xl" style="max-width: 400px">
            <div class="text-bold q-mb-xl text-h4">Forgot password?</div>
            <div class="q-gutter-xs">
                <q-input filled v-model="name" label="name" lazy-rules
                    :rules="[val => val && val.length > 0 || 'Please type something']" />
                <q-input filled v-model="id" label="id/e-mail" lazy-rules
                    :rules="[val => val && val.length > 0 || 'Please type something']">
                </q-input>
            </div>

            <div class="column q-gutter-y-md">
                <q-btn @click="Login" label="확인" type="submit" color="black" />
            </div>
        </div>
    </div>
</template>

<script setup>
import { api } from "src/boot/axios";
import { ref } from "vue";
import { useRouter } from "vue-router";

const $router = useRouter()
const name = ref()
const id = ref()

// 비밀번호 찾기
function Login() {
    if (!id.value || !name.value) {
        alert("모든 값을 입력해주세요.");
    }
    else {
        api.post('/auth/find-password', { email: id.value })
            .then((res) => {
                console.log(res);
            })
            .catch((error) => {
                console.error(error);
            });
    
        $router.push('login')
    }
}

</script>
