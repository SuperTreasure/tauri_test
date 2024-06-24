<script setup lang="ts">
import { ref, onMounted } from "vue";
import { invoke } from "@tauri-apps/api/tauri";

const greetMsg=ref( "" );
const name=ref( "" );

const data=ref<string|null>( null )

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  greetMsg.value=await invoke( "greet", { name: name.value } );
}
async function aaa() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  data.value=await invoke( "aaa", { name: name.value } );
}

onMounted( () => {
  aaa()
} )
</script>

<template>
  <form class="row" @submit.prevent="greet">
    <input id="greet-input" v-model="name" placeholder="Enter a name..." />
    <button type="submit">Greet</button>
  </form>

  <p>{{greetMsg}}</p>
  <p>{{data}}</p>
</template>
