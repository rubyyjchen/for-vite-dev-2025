<script setup>
    import { ref } from 'vue'; // ref 動態響應變數，即時更新
    const a = ref(1);
    const b = ref(2);        

    const inputValue = ref(3);
    function showValue() {
        alert(`你輸入的是：${inputValue.value}`);
    }


    const students = ref([
    { id: 's001', name: '洧杰', score: 90 },
    { id: 's002', name: '小花', score: 85 },
    { id: 's003', name: '阿明', score: 78 },
    { id: 's004', name: '佩佩', score: 92 }
    ])
</script>
<template>
    <!-- 讀取值 -->
    <input type="text" v-bind:value="a"></input>
    <!-- 雙向綁定 -->
    <input type="text" v-model="b"></input>
    <h1>標題 - {{ a }} & {{ b }}</h1>
    <hr>
    <input v-bind:value="inputValue" type="text"  />
    <p>{{ inputValue }}</p>
    <p>{{ inputValue }}</p>
    <p>{{ inputValue }}</p>
    <p>{{ inputValue }}</p>
    <p>{{ inputValue }}</p>
    <!-- on : 監聽事件，可觸發 function -->
    <button v-on:click="showValue" >顯示輸入值</button>
    <p >目前輸入：{{ inputValue }}</p>
    <hr>
    <div class="p-6">
    <h2 class="text-xl font-bold mb-4">👨‍🎓 學生名單</h2>
        <ul>
        <li v-for="student in students" :key="student.id" class="mb-2 p-2 border rounded">
            <p>🆔 學號：{{ student.id }}</p>
            <p>📛 姓名：{{ student.name }}</p>
            <p>📈 分數：{{ student.score }}</p>
        </li>
        </ul>
    </div>
</template>
<style scoped>
    h1{
        inline-size: 1.5;
    }
</style>