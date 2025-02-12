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

        <div class="flex flex-center">
            <div class="q-pa-md" style="max-width: 400px">
                <div class="text-bold q-mb-lg text-h4">Sign-up</div>
                <div class="q-gutter-xs">
                    <q-input filled v-model="name" label="name" lazy-rules
                        :rules="[val => val && val.length > 0 || 'Please type something']" />
                    <div class="row items-center">
                        <q-input filled v-model="id" label="id/e-mail" lazy-rules
                            :rules="[val => val && val.length > 0 || 'Please type something']">
                            <template v-slot:append>
                                <q-btn @click="checkEmail" label="이메일 인증" type="submit" color="black" class="q-my-xs" />
                            </template>
                        </q-input>
                    </div>
                    <q-input filled v-model="code" label="인증 코드" lazy-rules
                        :rules="[val => val && val.length > 0 || 'Please type something']">
                    </q-input>

                    <q-input filled type="password" v-model="pwd" label="password" lazy-rules :rules="[
                        val => val !== null && val !== '' || 'Please type your password',
                    ]" />
                    <q-input filled type="password" v-model="checkPwd" label="재입력" lazy-rules :rules="[
                        val => val !== null && val !== '' || 'Please type your password',
                    ]" />
                    <q-input filled v-model="phone" label="phone" lazy-rules
                        :rules="[val => val && val.length > 0 || 'Please type something']" />

                    <div class="column q-gutter-y-md">
                        <q-btn @click="Signup" label="Signup" type="submit" color="black" />
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

const $router = useRouter()
const name = ref()
const id = ref()
const code = ref()
const pwd = ref()
const checkPwd = ref()
const phone = ref()
const data = ref()

// 회원가입(인증코드 전송) 
function checkEmail() {
    api.post('/auth/register', { email: id.value }) //checkEmail() 함수는 이메일을 서버에 POST 요청으로 보냄, 요청 URL: /auth/register, 요청 본문(body): { email: id.value }
        .then((res) => {
            console.log(res);
        })
        .catch((error) => {
            console.error(error);
        });
}

// 회원가입
function Signup() {
    api.post('/auth/finalize-registration', { email: id.value,
        password: pwd.value,
        nickname: name.value,
        phone: phone.value,
        verificationCode: code.value
    })
        .then((res) => {
            console.log(res);
        })
        .catch((error) => {
            console.error(error);
        });

    if (!name.value || !id.value || !pwd.value || !checkPwd.value) {
        alert("모든 값을 입력해주세요.");
    }
    else {
        if (pwd.value === checkPwd.value) { //비밀번호 확인
            data.value = { //회원가입 데이터 생성
                nickName: name,
                email: id,
                password: pwd
            }
            console.log(data.value)
            $router.push('/')
        }
        else {
            alert("비밀번호가 일치하지 않습니다")
        }
    }

}

</script>