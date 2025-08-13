<template>
    <h1>複習</h1>
    <div>
        <input type="text" v-model="newName">
        {{ newName }}
        <input type="number" v-model="newNumber">
        {{ newNumber }}
        <button type="button" @click="addProduct">新增到資料集裡面</button>
    </div>
    <table>
        <thead>
            <tr>
                <th>標題</th>
                <th>價格</th>
                <th>調整價格</th>
                <th>刪除</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in data" :key="item.id">
                <td>{{ item.name }}</td>
                <td>{{ item.price }}</td>
                <td>
                    <input type="number" v-model="item.price"></input>
                </td>
                <td>
                    <button type="button" @click="deleteProduct(item.id)">刪除</button>
                </td>
            </tr>
        </tbody>
    </table>
    <h2>總價: {{ sum }}</h2>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import axios from 'axios';

const newName = ref('');
const newNumber = ref(0);
const data = ref([]);

const addProduct = () => {
    console.log("add Product:", newName.value, newNumber.value);
    data.value.push({
        id: data.value.length + 1,
        name: newName.value,
        price: newNumber.value
    });
    newName.value = '';
    newNumber.value = 0;
}

const deleteProduct = (id) => {
    console.log("delete Product:", id);
    const index = data.value.findIndex(item => item.id === id);
    data.value.splice(index, 1);
}

// 第一次畫面載入就會執行，如果 computed 裡面有使用 ref 的話，會自動追蹤資料的變化，
// 如果變數有變更，會自動觸發 computed 的重新計算
const sum = computed(() => {
    console.log("sum:", data.value);
    let tempSum = 0;
    data.value.forEach(item => {
        tempSum += item.price;
    });
    return tempSum;
});

// 等到 HTML 渲染完成後再去執行 mounted
// 通常會在 mounted 取得外部資料
onMounted(() => {
    console.log("mounted");
    setTimeout(() => {
        data.value = [            
            { id:1, name: '珍珠奶茶', price: 50},
            { id:2, name: '冬瓜檸檬', price: 45},
            { id:3, name: '翡翠檸檬', price: 55},
            { id:4, name: '四季春茶', price: 45},
            { id:5, name: '阿薩姆奶茶', price: 50},
            { id:6, name: '檸檬冰茶', price: 45},
            { id:7, name: '芒果綠茶', price: 55},
            { id:8, name: '抹茶拿鐵', price: 60} 
        ];
    }, 5000);
});

// JavaScript是逐行執行
// 但若使用 setTimeout 或 AJAX，會被放到事件佇列中，等到條件滿足或資料回傳才會觸發
console.log("1");
setTimeout(() => {
    console.log("2");
}, 0);
console.log("3");

// AJAX 請求
async function getData() {
    console.log("getData");
    const response = await axios.get('https://randomuser.me/api/');
    // 因為是 async 函數，所以會等 await response 回傳後再繼續
    console.log("test1");
    // 使用 await 可以確保在取得資料後才繼續執行後續程式碼。
    console.log("response:", response); 
};

// 1. 印出 "getData"
// 2. 等待 API 回應 (await)
// 3. 印出 "test1"
// 4. 印出 response 物件
getData();

function getData2() {
    console.log("getData2");
    const response2 = axios.get('https://randomuser.me/api/');
    console.log("test2");
    console.log("response2:", response2); 
};

// 1. 印出 "getData2"
// 2. 印出 "test2"
// 3. 印出 response2 (Promise 物件) -> Promise { <pending> }
// 4. API 回應還沒回來
getData2();
</script>

<style>

</style>