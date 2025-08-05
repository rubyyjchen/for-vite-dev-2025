<script setup>
import { ref } from 'vue'
// v-for 搭配陣列
const array = ref([
    {
        id:'1',
        name: "小明",
        age: 18,
    },
    {
        id:2,
        name: "小美",
        age: 16,
    },
    {
        id:'3',
        name: "漂亮阿姨",
        age: 20,
    },
])
// v-if, v-else, v-show
const isChecked = ref(false)

</script>
<template>
    <div>
        <!-- 一定要加上 key，會影響渲染效率、結果 -->
        <div v-for="(item, key) in array" :key="item.id">
            索引：{{ key }} |
            姓名：{{ item.name }} |
            年齡：{{ item.age }} |
            <!-- v-if 不要跟 v-for 一起使用（同一層），可在內層或外層 -->
            <div>
                <h1 v-if="item.age > 18">大於 18 歲</h1>
                <h1 v-else>小於 18 歲</h1>
            </div>
        </div>
        <hr>
        <input type="checkbox" v-model="isChecked">{{ isChecked }}
        <!-- v-if 在條件不符合時會將元素移除 -->
        <h1 v-if="isChecked">當 isChecked 為 true 時，會顯示這行</h1>
        <h1 v-else="isChecked">目前的 isChecked 為 falese</h1>
        <!-- v-show 元素一直都是存在的，在條件不符合時只是會被隱藏 display:none -->
        <h1 v-show="isChecked">當 isChecked 為 true 時，會顯示這行</h1>
    </div>
</template>