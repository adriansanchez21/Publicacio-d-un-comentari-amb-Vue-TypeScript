<template>
  <div>
    <form>
      <ul class="emoticon-list">
        <li v-for="emoticon in emoticonList" :key="emoticon.name">
          <label :for="emoticon.name">
            <input type="radio" :id="emoticon.name" :value="emoticon.imageUrl" v-model="selectedEmoticon" name="emoticons" @change="selectEmoticon(emoticon.imageUrl)" />
            <img :src="emoticon.imageUrl" :alt="emoticon.name" :class="{ 'selected': selectedEmoticon === emoticon.imageUrl }" />
          </label>
        </li>
      </ul>
    </form>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type Emoji from "@/types/Emoji.ts";

const emoticonList: Emoji[] = [
  { name: 'happy', imageUrl: './src/assets/emojis/happy.png' },
  { name: 'sad', imageUrl: './src/assets/emojis/sad.png' },
  { name: 'surprised', imageUrl: './src/assets/emojis/surprised.png' }
];


const selectedEmoticon = ref<string | null>(null);

const selectEmoticon = (imageUrl: string) => {
  selectedEmoticon.value = imageUrl;
  emit('emoticonSelected', imageUrl);
};

const emit = defineEmits(['emoticonSelected']);

const emitToFormulari = (imageUrl: string) => {
  emit('emoticonSelected', imageUrl);
};
</script>

<style scoped>
.emoticon-list {
  list-style: none;
  padding: 0;
}

.emoticon-list li {
  display: inline-block;
  margin: 5px;
}

img {
  width: 40px;
  height: 40px;
  cursor: pointer;
}
</style>