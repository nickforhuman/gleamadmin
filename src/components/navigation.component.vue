<script setup>
import {ref} from "vue"
import { useRoute } from "vue-router"
// icons
import menuIcon from "./icons/menu.icon.vue"

const navItems = ref([
    {name: "PC server", link: "/"},
    {name: "VPS", link: "/add/vps"},
    {name: "Web Host", link: "/add/hosting"},
    {name: "NASS", link: "/add/nass"},
])

// controls
const isNavigation = ref(true);

const navOpen = () => {
    isNavigation.value = !isNavigation.value
}
</script>
<template>
 <transition name="nav"> 
   <div class="w-1/2 h-screen fixed select-none top-0 left-0 bg-primary/60 backdrop-blur-md border-l-2 border-forty" v-if="!isNavigation">
        <div class="w-full">
            <div @click="navOpen" class="flex m-2 hover:rotate-180 hover:bg-primary hover:text-forty transition-all items-center justify-center p-2 w-8 h-8 rounded-full bg-primary cursor-pointer">
                <h1 class="text-forty font-bold">X</h1>
            </div>
            <div class="w-full flex justify-center items-center">
                <ul class="w-full flex flex-col justify-center items-center gap-5">
                    <li v-for="(navItem, index) in navItems" class="w-full p-6 border-b-2 border-forty text-forty hover:bg-forty hover:text-primary transition-all font-bold text-xl" :key="index">
                        <router-link :to="navItem.link">
                            {{ navItem.name }}
                        </router-link>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</transition>
<div class="fixed bottom-1 left-1 p-4 cursor-pointer bg-forty/70 backdrop-blur-md" @click="navOpen">
    <menuIcon class="w-6 h-6 fill-primary"/>
</div>
</template>


<style scoped>
.nav-enter-from {
  transform: translateX(-100%);
}
.nav-enter-active {
  transition: transform 0.3s ease;
}
.nav-enter-to {
  transform: translateX(0);
}

.nav-leave-from {
  transform: translateX(0);
}
.nav-leave-active {
  transition: transform 0.3s ease;
}
.nav-leave-to {
  transform: translateX(-100%);
}
</style>