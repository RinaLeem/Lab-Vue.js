<script setup>
import {ref, onMounted} from 'vue';

const myNumber = ref('');
const numberType = ref('');
const fact = ref(null);

const loading = ref(false);
const show = ref(false);

async function handleSearch() {
    loading.value = true;
    try {
        fact.value = await getInfo(myNumber.value, numberType.value);
    } catch (e) {
        console.error('Error', e)
    } finally {
        loading.value = false;
    }
}
function getInfo(num, type = 'trivia' ) {
    return fetch(`http://numbersapi.com/${num}/${type}?json`, {
        method: 'GET',
    })
        .then(response => response.json())
}

onMounted(() => {
    handleSearch();
})

const getMessage = () => {
    if (numberType.value === 'year') {
        return 'скучный год';
    } else {
        return 'скучное число';
    }
};

function findFact(){
    show.value = true;
    handleSearch();
}

</script>

<template>
    <main>
        <div class="container">
            <h1>Случайные факты о числах</h1><br>        

            <form @submit.prevent="handleSearch">
                <input type="number" v-model.number="myNumber" placeholder="Введите число"/><br>
                <input type="text" list="types" v-model="numberType" placeholder="Тип факта" ><br>
                <datalist id="types">
                    <option value="math"></option>
                    <option value="year"></option>
                    <option value="trivia"></option> 
                </datalist><br>
                <input type="button" @click="findFact" value="Искать" class="button"><br><br>
            </form> 

            <div v-if="show">
                <div v-if="loading">Загрузка...</div>
                <div v-else-if="fact.found">{{ fact.text }} </div>
                <div v-else>{{myNumber}} - {{getMessage()}} </div>
            </div>
            
        </div>
    </main>
</template>

<style scoped>
.container{
    width: 500px;
    border: 4px;
    border-style:groove;
    padding: 20px;
}
input{
    width: 150px;
    background-color:rgb(232, 238, 241);
}
.button{
    height: 40px;
    margin-top: 10px;
    background-color:rgb(198, 217, 224);
}

</style>
