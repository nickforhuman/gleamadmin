<script setup>
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/core";
import {RouterView} from "vue-router";
import navigationComponent from "./components/navigation.component.vue";

const greetMsg = ref("");
const name = ref("");

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/develop/calling-rust/
  greetMsg.value = await invoke("greet", { name: name.value });
}

</script>

<template>
<div id="container" class="w-full min-h-screen bg-primary">
  <RouterView/>
  <navigationComponent/>
</div>
</template>

