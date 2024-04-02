<script setup>
import {ref, computed} from 'vue';

const tasks = ref ([]);
const taskText = ref('');
let id = 0;

function addToList() {
    tasks.value.push({ text: taskText.value, isDone: false, id: id++ });
    taskText.value = '';
    taskAmound.value = 0;
}




</script>

<template>
    <main>
        <div>
            <h1>Список дел</h1>
            

            <form @submit.prevent="addToList">
                <input type="text" v-model.trim="taskText" placeholder="Введите название"/> <br>
                <input type="button" @click="addToList" value="Добавить"><br><br>
            </form>

            <div v-for="item of tasks" :key="item.id">
                <label :for="item.id">{{ item.text }}</label>
            </div>
               

        </div>
        


    </main>
</template>

<style scoped>

</style>
