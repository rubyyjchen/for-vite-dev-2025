<script setup>
import { ref } from 'vue';
const menu = ref({
    columnName: [
        { name: '品項', field: 'name' },
        { name: '描述', field: 'description' },
        { name: '價格', field: 'price' },
        { name: '庫存', field: 'stock' },
        { name: '編輯', field: 'edit' }
    ],
    items: [
        { id:1, name: '珍珠奶茶', description: '香濃奶茶搭配QQ珍珠', price: 50, stock: 20, isEditing: false, originalName: '' },
        { id:2, name: '冬瓜檸檬', description: '清新冬瓜配上新鮮檸檬', price: 45, stock: 18, isEditing: false, originalName: '' },
        { id:3, name: '翡翠檸檬', description: '綠茶與檸檬的完美結合', price: 55, stock: 34, isEditing: false, originalName: '' },
        { id:4, name: '四季春茶', description: '香醇四季春茶，回甘無比', price: 45, stock: 10, isEditing: false, originalName: '' },
        { id:5, name: '阿薩姆奶茶', description: '阿薩姆紅茶搭配香醇鮮奶', price: 50, stock: 25, isEditing: false, originalName: '' },
        { id:6, name: '檸檬冰茶', description: '檸檬與冰茶的清新組合', price: 45, stock: 20, isEditing: false, originalName: '' },
        { id:7, name: '芒果綠茶', description: '芒果與綠茶的獨特風味', price: 55, stock: 18, isEditing: false, originalName: '' },
        { id:8, name: '抹茶拿鐵', description: '抹茶與鮮奶的絕配', price: 60, stock: 20, isEditing: false, originalName: '' }
    ]
});

const add = (item) => {
    item.stock++;
};
const less = (item) => {
    item.stock--;
    item.stock = item.stock < 0 ? 0 : item.stock;
};
const edit = (item) => {
    if (!item.isEditing) {
        item.originalName = item.name;
        item.isEditing = true;
    } else {
        item.isEditing = false;
    }
};
const cancelEdit = (item) => {
    item.name = item.originalName;
    item.isEditing = false;
};
</script>
<template>
    <div>
        <h1>HW1</h1>
        <hr>
        <table>
            <thead>
                <tr>
                    <th v-for="colName in menu.columnName" :key="colName.description" scope="col">{{ colName.name }}</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in menu.items" :key="item.id">
                    <td>
                        <label v-if="!item.isEditing">{{ item.name }}</label>
                        <input v-if="item.isEditing" type="text" :readonly="!item.isEditing" v-model="item.name">
                    </td>
                    <td><small>{{ item.description }}</small></td>
                    <td>{{ item.price }}</td>
                    <td>
                        <button @click="less(item)">-</button>
                        {{ item.stock }}
                        <button @click="add(item)">+</button>
                    </td>
                    <td>
                        <button type="button" @click="edit(item)">
                            {{ item.isEditing ? '儲存' : '編輯' }}
                        </button>
                        <button v-if="item.isEditing" type="button" @click="cancelEdit(item)">取消</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>