<script setup lang="ts">
import Formulari from "./components/Formulari.vue";
import Enviat from "./components/Enviat.vue"
import type Entry from "./types/Entry";

import { reactive, ref } from "vue";

const entrades: Entry[] = reactive([]);

const manipularPost = (entradaPost: Entry) => {
  entrades.push(entradaPost)
  console.log(entradaPost)
}

</script>

<template>
  <h1>My Journal</h1>
  <div class="principal">
    <Formulari @@create="manipularPost"></Formulari>
  </div>
  <ul>
    <li v-for="entrada in entrades" :key="entrada.id">
      <Enviat :entrada="entrada"/>
    </li>
  </ul>
</template>

<style scoped>
.principal{
  width: 800px;
  text-align: center;
  background-color: #e5e7eb;
}

li {
  list-style-type: none;
}

ul{
  padding: 0;
}
</style>