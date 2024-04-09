<script setup>
import {ref, computed} from 'vue';

const history = ref ([]);
const taskText = ref('');
const taskAmound = ref('');
let id = 0;

function addToList() {
    if (taskText.value != '' && taskAmound.value != '') {
        history.value.push({ text: taskText.value, amound: taskAmound.value, id: id++ });
        taskText.value = '';
        taskAmound.value = 0;
    }
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
        <div class = "container">
            <h1>Учет расходов</h1> <br>
            <div v-if="history.length" class="balance">
                <label name="balance">Баланс: </label>
                <span name="balance" >{{totalBalance}}</span><br>
                <label name="income">Доходы: </label>
                <span name="income">{{incomeBalance}}</span><br>
                <label name="expenses">Расходы: </label>
                <span name="expenses">{{outcomeBalance}}</span><br>
                
            </div>
            <template v-else>
                <h4>Вы не совершали финансовых операций</h4>
            </template><br>
            
            
            <form @submit.prevent="addToList">
                <input type="text" v-model.trim="taskText" placeholder="Введите название"/> <br>
                <input  type="number" v-model.number="taskAmound" placeholder="Введите сумму"/> <br>
                <input type="button" @click="addToList" value="Добавить" class="button"><br><br>
            </form>  

            <div v-for="item of history" :key="item.id" class="list"><hr>
                <label :for="item.id"> {{ item.text }} <span class="task_amound" :class = 'item.amound>0 ? "plus":"minus"'>{{ item.amound }}</span></label> 
            </div>
               

        </div>
    </main>
</template>

<style scoped>
.container{
    width: 400px;
    border: 4px;
    border-style:groove;
    padding: 20px;
    
}
.balance{
    border-style:groove;
    padding: 5px;
    
}
input{
    width: 350px;
    background-color:rgb(219, 234, 240);

}
.button{
    height: 40px;
    margin-top: 10px;
    background-color:rgb(198, 217, 224);
}
.list{
    width: 350px;
    position: relative;
}
.task_amound{
    position: absolute;
    right: 0px;
}

.plus{
    color: green;
}
.minus{
    color:red;
}

</style>
