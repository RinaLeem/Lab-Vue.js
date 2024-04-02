<script setup>
// JS код тут
import {ref, reactive} from 'vue';

const history = reactive ([]);
const history_element = {
    text: '',
    amound: 0,
    id: 0.
}

class element{
    constructor(text,amound,id){
        this.text = text;
        this.amound = amound;
        this.id = id;
    }
}


</script>

<template>
  <!-- HTML код тут -->
    <main>
        <div class="menu">
           <h1>Учет расходов</h1>
           
           <label name="balance">Баланс</label>
           <span>0</span>

        </div>


    </main>
</template>

<style scoped>
/* CSS код тут */

</style>
