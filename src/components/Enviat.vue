<template>
  <div>
    <div class="img-emoji">
      <img src="../assets/emojis/surprised.png" alt="">
      <!-- Lo de mostrar els emojis no ho he aconseguit, he posat la imatge a ma per a que visualment es vegi com quedaria però aquesta part no la he aconseguit fer -->
    </div>
    <div class="text">
      <span>{{ entrada.body }}</span>
    </div>
      <p>{{ mostrarData(entrada.dataCreacio) }}</p>
  </div>
</template>


<script setup lang="ts">
import { defineProps, ref } from 'vue';
import type Entry from "@/types/Entry.ts";

const props = defineProps({
  entrada: {
    type: Object as () => Entry,
    required: true
  }
});


const mostrarData = (dateTime: string | number | Date) => {
  const data = new Date(dateTime);

  const dia = data.getDate();
  const mes = data.getMonth() + 1;
  const any = data.getFullYear();
  const hores = data.getHours();
  const minuts = data.getMinutes();

  const formattedTime = `${dia}/${mes}/${any} at ${hores}:${minuts}`;
  return formattedTime;
};

</script>

<style scoped>


div{
  background-color: #e5e7eb;
  display: flex;
  margin: 10px;
  margin-left: 0px;
  width: 800px;
}

img{
  max-width: 80%;
  margin-left: 10%;
}

.img-emoji {
  width: 20%;
  background-color: #e5e7eb;
}
.text {
  width: 50%;
  background-color: #e5e7eb;
}
</style>