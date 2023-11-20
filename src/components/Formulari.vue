<template>
    <form @submit.prevent="gestionarSubmit">
        <textarea :value="body"
        @keyup="recollirTextForm"
        name="" id="" cols="80" rows="10" maxlength="280"></textarea>
        <br>
        <Emoticonos/>
        <span>{{ charCount }} / {{maxCaracters}}</span>
        <button type="submit">Remember</button>
    </form>
</template>

<script setup lang="ts">
import { computed, ref, toHandlerKey, inject, onMounted } from 'vue';
import Emoticonos from '@/components/Emoticonos.vue'
import type Entry from "@/types/Entry.ts";
import type Emoji from "@/types/Emoji.ts";

const emit = defineEmits<{
    (e: "@create", entry:Entry): void
}>();

const maxCaracters = 280
const body = ref("")
const emoji = ref <Emoji | null> (null)
const charCount = computed(() => body.value.length)
console.log(charCount)

const recollirTextForm = (e: Event)=>{
    const textarea = e.target as HTMLTextAreaElement
    if (textarea.value.length<=maxCaracters){
        body.value = textarea.value
    }
}

const gestionarSubmit = ()=>{
    emit('@create', {
        body: body.value, 
        emoji: emoji.value, 
        dataCreacio: new Date(), 
        userId: 1, 
        id: Math.random()})
}

</script>

<style scoped>
form {
    padding: 10px;
}
</style>