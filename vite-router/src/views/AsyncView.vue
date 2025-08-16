<template>
    <h1>Async Function</h1>
</template>

<script setup>
// JS 是逐行執行，但非同步是所有程式碼跑完才執行
// 執行順序： 1 -> 3 -> 2
// console.log('1');

// setTimeout(() => {
//     console.log('2');
// }, 0);

// console.log('3');

// 如何可以確保他按順序執行
// setTimeout(() => {
//     console.log('4');
// }, 5);
// setTimeout(() => {
//     console.log('5');
// }, 10);
// setTimeout(() => {
//     console.log('6');
// }, 7);

//1. 波動拳程式碼 (callback function)
// setTimeout(() => {
//     console.log('4');
//     setTimeout(() => {
//         console.log('5');
//         setTimeout(() => {
//             console.log('6');
//         }, 7);
//     }, 10);
// }, 5);

//2. Promise base 搭配 async/await
//async/await 使用前提：必須要搭配 Promise
//ex. setTimeout、jQuery Ajax 是 callback
//ex. fetchAPI 是 Promise base
//ex. axios 是 Promise base -> npm install axios

import axios from 'axios';
//promise 的用法、需要依序執行時
// axios.get('https://randomuser.me/api/') // 第一次發出的請求
//     .then(response => {
//         console.log('1-response:', response);
//         return axios.get('https://randomuser.me/api/'); // 第二次發出的請求
//     })
//     .then(response => {
//         console.log('2-response:', response);
//         return axios.get('https://randomuser.me/api/'); // 第三次發出的請求
//     })
//     .then(response => {
//         console.log('3-response:', response);
//     })
//     .catch(error => {
//         console.log('error:', error);
// });

//async/await
function getData1(){
    console.log('1');
    //先定義要取得什麼資料、執行甚麼方法
    const response = axios.get('https://randomuser.me/api/');
    console.log('2');
    console.log(response); // promise pending，因為promise是非同步事件，程式最後才執行
    console.log('3');
}

getData1();

//async/await
async function getData2(){
    console.log('getData async:');
    //先定義要取得什麼資料、執行甚麼方法
    const response = await axios.get('https://randomuser.me/api/');
    console.log('1-response:', response); // await 加入後會變逐行執行 
    const response2 = await axios.get('https://randomuser.me/api/');
    console.log('2-response:', response2);
    const response3 = await axios.get('https://randomuser.me/api/');
    console.log('3-response:', response3);
}

getData2();

</script>

<style scoped>

</style>