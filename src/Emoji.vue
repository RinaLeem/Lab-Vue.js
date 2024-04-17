<script setup>
import { defineProps } from 'vue';

const props = defineProps({
 emoji: Object
});
</script>

<template>
 <span v-html="emoji.htmlCode[0]" class="emoji-icon"></span>
 </template>

<style scoped>
.emoji-icon {
 font-size: 80px;
 margin: 30px;
}
</style>