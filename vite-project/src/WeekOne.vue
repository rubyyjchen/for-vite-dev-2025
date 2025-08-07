<script setup>
import { ref } from 'vue';

const text = ref('這是一段文字');

const todos = ref([
  { id: 1, text: '123', imgUrl: 'https://images.unsplash.com/photo-1471295253337-3ceaaedca402?q=80&w=300&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D' },
  { id: 2, text: '456', imgUrl: 'https://images.unsplash.com/photo-1578432014316-48b448d79d57?q=80&w=300&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D' }
]);

const tempEdit = ref({
  id: 0,
  text: ''
});

const addTodo = () =>{
  todos.value.push({
    id: new Date().getTime(),
    text: text.value,
  });
  console.log(todos.value);
  text.value = '';
};

const deleteTodo = (todo) => {
  console.log(todo);
  const index = todos.value.findIndex(item => item.id === todo.id);
  console.log(index);
  todos.value.splice(index, 1);
};

const prepareEdit = (todo) => {
  // JS 的物件傳參考，所以tempEdit.value的值會隨todo的值改變而改變 （非Vue的鍋）
  // tempEdit.value = todo;
  // 所以需要使用 "拷貝" 的形式來避免連動
  tempEdit.value = {...todo};
  console.log(tempEdit.value);
};

const confirmEdit = () => {
  const index = todos.value.findIndex(item => item.id === tempEdit.value.id);
  todos.value[index] = tempEdit.value;
  tempEdit.value = {};
};
</script>
<template>

    <input type="text" v-model="text">
    <button type="button" @click="addTodo">新增</button>
    <div v-for="todo in todos" v-bind:key="todo.id">
        {{ todo.text }}
        <img :src="todo.imgUrl" alt="todo.text">
        <button type="button" @click="deleteTodo(todo)">刪除</button>
        <button type="button" @click="prepareEdit(todo)">編輯</button>
        <hr>
    </div>
    <div v-if="tempEdit.id">
        <h2>編輯區域</h2>
        當前修改的值：{{ tempEdit.text }} <br>
        <input type="text" v-model="tempEdit.text"></input>
        <button type="button" @click="confirmEdit">確認</button>
        <button type="button" @click="tempEdit = {}">取消</button>
    </div>

</template>