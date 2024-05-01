<script setup>
import { defineProps, computed } from 'vue';
import Emoji from './Emoji.vue'; 

// Принимаем данные
const props = defineProps({
 firstEmoji: Object,
 secondEmoji: Object
});

// Получаем новый эмоджи
const mixedEmoji = computed(() => {
 if (props.firstEmoji && props.secondEmoji) {
    const [unicodeFirst, unicodeSecond] = [props.firstEmoji.unicode[0], props.secondEmoji.unicode[0]].map(u => u.replace('U+', '').toLowerCase());
    return `https://emk.vercel.app/s/${unicodeFirst}_${unicodeSecond}?size=126`;
 }
});
</script>

<template>
  <div>
    <div v-if="firstEmoji" >
      <Emoji :emoji="firstEmoji" />
    </div>
    
    <div v-if="secondEmoji" >
      <Emoji :emoji="secondEmoji" />
    </div> <br>
    
    <img v-if="mixedEmoji" :src="mixedEmoji" alt="Mixed Emoji">
  </div>
 </template>

<style scoped>
img {
 font-size: 62px;
 margin: 30px;
}
span{
  font-size: 30px;
  text-align: center;
}
</style>

