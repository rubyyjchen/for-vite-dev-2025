<template>
    <h1>Review</h1>
    <div>
        <input type="text" v-model="newName">{{ newName }}</input>
        <input type="number" v-model="newNumber">{{ newNumber }}</input>
        <button type="button" @click="addProduct">新增到資料集內</button>
    </div>
    {{ data }}
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
    <h2>總和:{{ sum }}</h2>
    <button type="button" id="button">這是按鈕</button>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

const newName = ref('');
const newNumber = ref(0);

// 通常會在非同步的時候才加入，在 mounted 的時候觸發
// const data = ref(
//     [{ "id": 1, "name": "珍珠奶茶", "price": 50},
//     { "id": 2, "name": "冬瓜檸檬", "price": 45},
//     { "id": 3, "name": "翡翠檸檬", "price": 55},
//     { "id": 4, "name": "四季春茶", "price": 45},
//     { "id": 5, "name": "阿薩姆奶茶", "price": 50},
//     { "id": 6, "name": "檸檬冰茶", "price": 45},
//     { "id": 7, "name": "芒果綠茶", "price": 55},
//     { "id": 8, "name": "抹茶拿鐵", "price": 60}
// ]);

const data = ref([]);

const addProduct = () => {
    data.value.push({
        id: new Date().getTime(),
        name: newName.value,
        price: newNumber.value
    });
    newName.value = '';
    newNumber.value = 0;
}

const deleteProduct = (id) => {
    const index = data.value.findIndex(item => item.id === id);
    data.value.splice(index, 1);
}

// 使用 reduce 計算總和
// reduce 的參數為一個函數，第一個參數為前一個值，第二個參數為當前值，第三個參數為當前索引，第四個參數為當前陣列
// const sum = computed(() => {
//     const tempSum = data.value.reduce((pre, item) =>{
//         console.log(pre, item);
//         return pre + item.price; //第一次為外部傳入:0，第二次為前一個 return 的值
//     }, 0);

//     // let tempSum = 0;
//     // data.value.forEach(item => {
//     //     tempSum += item.price;
//     // });
//     // return tempSum;
// })


const sum = computed(() => {
    return data.value.reduce((pre, item) =>{
        return pre + item.price;
    }, 0);
})

let intervalId = 0;
onMounted(() => {
    //AJAX
    // 模擬非同步的資料，在 1 秒後才取得資料
    setTimeout(() => {
        data.value = [
            { "id": 1, "name": "珍珠奶茶", "price": 50},
            { "id": 2, "name": "冬瓜檸檬", "price": 45},
            { "id": 3, "name": "翡翠檸檬", "price": 55},
            { "id": 4, "name": "四季春茶", "price": 45},
            { "id": 5, "name": "阿薩姆奶茶", "price": 50},
            { "id": 6, "name": "檸檬冰茶", "price": 45},
            { "id": 7, "name": "芒果綠茶", "price": 55},
            { "id": 8, "name": "抹茶拿鐵", "price": 60}
        ]
    }, 1000);    

    // 重複觸發，到別的頁面還會繼續觸發
    // intervalId = setInterval(() => {
    //     console.log(1);
    // }, 500);

    const btn = document.querySelector('#button');
    console.log('btn:', btn);
})

// 換頁的時候會觸發 Unmounted，會把 intervalId 清除
onUnmounted(() => {
    clearInterval(intervalId);
})

// 這個抓不到，要在 mounted 的時候抓
// const btn = document.querySelector('#button');
// console.log('btn:', btn);

// 再寫一個 onMounted 也不會出錯
// Option API 有固定放的位置 -> Vue2
// Composition API 可以看你的意思決定 -> Vue3
onMounted(() => {
    const btn = document.querySelector('#button');
    console.log('btn:', btn);
})
</script>

<style>

</style>