<script setup>
import {ref, computed} from 'vue';

const tasks = ref ([]);
const taskText = ref('');
let id = 0;

function addToList() {
    tasks.value.push({ text: taskText.value, isDone: false, id: id++ });
    taskText.value = '';
}

function deleteFromList(id) {
    const taskIndex = tasks.value.findIndex(task => task.id === id);
    tasks.value.splice(taskIndex, 1);
}

function editTask(id) {
    const newText = prompt();
    if (newText = '') {
        const taskIndex = tasks.value.findIndex(task => task.id === id);
        tasks.value[taskIndex].text = newText;
    }
}


</script>

<template>
    <main>
        <div>
            <h1>Список дел</h1>
            
            <div class = "container">
                <form @submit.prevent="addToList">
                    <input type="text" v-model.trim="taskText" placeholder="Введите название"/> <br>
                    <input type="button" @click="addToList" value="Добавить"><br><br> <hr>
                </form>

                <div v-if="tasks.length">
                    <div v-for="item of tasks" :key="item.id">
                        <label :for="item.id">{{ item.text }}</label>
                        <button @click="editTask(item.id, item.text)" class = edit_button>Изменить</button>
                        <button @click="deleteFromList(item.id)" class = delete_button>Удалить</button>
                        <hr>
                    </div>

                </div>
                <template v-else>
                    <h4>Список дел пуст</h4>
                </template>
            
            </div>
            
        </div>
        


    </main>
</template>

<style scoped>
.container{
    width: 400px;
    position: relative;
}
.edit_button{
    position: absolute;
    right: 70px;
    background-color: rgb(224, 245, 255);
}
.delete_button{
    position: absolute;
    right: 0px;
    background-color:rgb(255, 192, 192);
}

</style>
