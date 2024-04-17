<script setup>
import {ref, onMounted} from 'vue';
import Emoji from './Emoji.vue';
import EmojiList from './EmojiList.vue'
import EmojiMixer from './EmojiMixer.vue';

const emojis = ref([]);
const selectedEmojis = ref([null, null]);

onMounted(() => {
    loadEmojis();
})

// Загрузка эмоджи
async function loadEmojis() {
    const response = await fetch(`https://emojihub.yurace.pro/api/all`);
    const data = await response.json();
    emojis.value = data;
    selectedEmojis.value = [data[83], data[82]];
}



// Выбор эмоджи
function handleSelectEmoji(index, selectedEmoji) {
 console.log('Selected emoji:', selectedEmoji);
 selectedEmojis.value[index] = selectedEmoji;
}

</script>

<template>
    <main>
        <div class="container">
           
            <EmojiList id="left" :emojis="emojis" @selectEmoji="(emoji) => handleSelectEmoji(0, emoji)" />
                
            <EmojiMixer :firstEmoji="selectedEmojis[0]" :secondEmoji="selectedEmojis[1]" />

            <EmojiList id="right" :emojis="emojis" @selectEmoji="(emoji) => handleSelectEmoji(1, emoji)" />

            
        </div>
    </main>
</template>


<style scoped>
.container {
 display: flex;
  justify-content: center;
}
.emoji-lists {
 display: flex;
 justify-content: space-between;
 width: 100%;
}
#left{
margin-right: 50px;
}

</style>