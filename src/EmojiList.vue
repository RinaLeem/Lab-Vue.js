<script setup>
import { defineProps } from 'vue';

// Входные параметры
const props = defineProps({
 emojis: Array
});
// Выходные параметры
const emit = defineEmits(['selectEmoji']);
// Выбор эмоджи
function selectEmoji(index, emoji) {
 emit('selectEmoji', index, emoji);
}
</script>

<template>
 <div class="emoji-list">
    <div v-for="(emoji, index) in emojis" :key="index" @click="selectEmoji(emoji)">
      <span v-html="emoji.htmlCode[0]"></span>
    </div>
 </div>
</template>

<style scoped>
.emoji-list {
 display: grid;
 grid-template-columns: repeat(12, 15px);
 gap: 20px;
 font-size: 32px;
}
</style>

