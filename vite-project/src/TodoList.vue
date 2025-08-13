<template>
    <h1>代辦</h1>
    <h2>註冊功能</h2>
    <input type="email" placeholder="請輸入email" v-model="signupField.email"></input>
    <input type="text" placeholder="請輸入密碼" v-model="signupField.password"></input>
    <input type="text" placeholder="請輸入暱稱" v-model="signupField.nickname"></input>
    <br>
    {{ signupField }}
    <br>
    <button @click="signup">註冊</button>
    <br>
    {{ signupResponse }}
    <h2>登入功能</h2>
    <input type="email" placeholder="請輸入email" v-model="loginField.email"></input>
    <input type="text" placeholder="請輸入密碼" v-model="loginField.password"></input>
    <br>
    {{ loginField }}
    <br>
    <button @click="login">登入</button>
    <br>
    Token:{{ loginResponse }}
    <br>
    <h2>驗證</h2>
    <div v-if="user.uid">
        <p>UID:{{ user.uid }}</p>
        <p>暱稱:{{ user.nickname }}</p>
    </div>
    <div v-else>
        <p>請先登入</p>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
import { onMounted } from 'vue';

const api = 'https://todolist-api.hexschool.io';

const signupField = ref({
    email: '',
    password: '',
    nickname: ''
});
const signupResponse = ref('');
const signup = async () => {
    try{
        const res = await axios.post(`${api}/users/sign_up`, signupField.value);
        console.log(res);
        signupResponse.value = res.data.uid;
    }catch(error){
        console.log(error);
        signupResponse.value = error.response.data;
    }
}

const loginField = ref({
    email: '',
    password: ''
});
const loginResponse = ref('');
const login = async () => {
    try{
        const res = await axios.post(`${api}/users/sign_in`, loginField.value);
        console.log(res);
        loginResponse.value = res.data.token;
        document.cookie = `customTodoToken=${res.data.token};path=/`;
    }catch(error){
        console.log(error);
        loginResponse.value = error.response.data;
    }
}

const user = ref({
    status: '',
    uid: '',
    nickname: ''
});

onMounted(async () => {
    // 取得token
    const token = document.cookie.replace(/(?:(?:^|.*;\s*)customTodoToken\s*\=\s*([^;]*).*$)|^.*$/, "$1");
    console.log(token);
    // 取得使用者資料
    const res = await axios.get(`${api}/users/checkout`, {
        headers: {
            Authorization: token
        }
    });
    console.log(res);
    user.value = res.data;
});
</script>

<style>
</style>