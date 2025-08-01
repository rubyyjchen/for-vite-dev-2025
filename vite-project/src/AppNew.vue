<script setup>
import { ref } from 'vue';

const text = ref('Ruby Chen');
const num = ref(1);
const imgSrc = ref('https://images.unsplash.com/photo-1471295253337-3ceaaedca402?q=80&w=300&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D');

const todos = ref([
  { id: 1, name: '購買雜貨', dueDate: '2024-07-30', completed: true },
  { id: 2, name: '完成報告', dueDate: '2024-08-01', completed: false },
  { id: 3, name: '清理房間', dueDate: '2024-07-28', completed: true },
  { id: 4, name: '計劃假期', dueDate: '2024-08-05', completed: false },
  { id: 5, name: '處理稅務', dueDate: '2024-08-10', completed: false }
]);

const add = () => {
  num.value++;
};
</script>
<template>
    <h1>{{ text }}</h1>
    <input v-model="text" />
    <h2>{{ num }}</h2>
    <!-- <button v-on:click="add">點我</button> -->
    <button @click="add">點我</button>

    <!-- <img v-bind:src="imgSrc" alt="baseball" /> -->
    <img :src="imgSrc" alt="baseball" />
    <br>
    <div>
        <div v-for="todo in todos" v-bind:key="todo.id">
            {{ todo.name }} <br>
            {{ todo.dueDate }} <br>
            {{ todo.completed ? '是' : '否' }}
            <input type="checkbox" v-model="todo.completed">
            <button type="button" @click="todo.completed = !todo.completed">切換</button>
            <hr>
        </div>
    </div>

</template>