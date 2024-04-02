<script setup>
import {ref, computed} from 'vue';

const history = ref ([]);
const taskText = ref('');
const taskAmound = ref(0);
let id = 0;

function addToList() {
    history.value.push({ text: taskText.value, amound: taskAmound.value, id: id++ });
    taskText.value = '';
    taskAmound.value = 0;
}

const incomeBalance = computed(() => {
    let totalIncome = 0;
    for (let task of history.value) {
        if (task.amound > 0) {
            totalIncome += task.amound;
        }
    }
    return totalIncome;
});

const outcomeBalance = computed(() => {
    let totalIncome = 0;
    for (let task of history.value) {
        if (task.amound < 0) {
            totalIncome += task.amound;
        }
    }
    return totalIncome;
});

const totalBalance = computed(() => {
    let totalIncome = 0;
    for (let task of history.value) {
        totalIncome += task.amound;
    }
    return totalIncome;
});



</script>

<template>
    <main>
        <div>
            <h1>Учет расходов</h1>
            <div v-if="history.length">
                <label name="balance">Баланс: </label>
                <span name="balance" >{{totalBalance}}</span><br>
                <label name="income">Доходы: </label>
                <span name="income">{{incomeBalance}}</span><br>
                <label name="expenses">Расходы: </label>
                <span name="expenses">{{outcomeBalance}}</span><br><br>
                
            </div>

            <form @submit.prevent="addToList">
                <input type="text" v-model.trim="taskText" placeholder="Введите название"/> <br>
                <input  type="number" v-model.number="taskAmound" placeholder="Введите сумму"/> <br>
                <input type="button" @click="addToList" value="Добавить"><br><br>
            </form>

            <div v-for="item of history" :key="item.id">
                <label :for="item.id">{{ item.text }}  {{ item.amound }}</label>
            </div>
               

        </div>
        


    </main>
</template>

<style scoped>

</style>
