<script setup>
import {ref} from "vue"
import plusIcon from "./icons/plus.icon.vue"

// settings
const isAddserver = ref(false);
const addServerToggle = () => {
    isAddserver.value = !isAddserver.value
}
</script>
<template>
    <!-- button start  -->
    <div @click="addServerToggle" class="w-full text-forty gap-2 p-2 flex justify-end items-center">
        Add Server
        <button class="cursor-pointer w-8 h-8 p-2 rounded-full bg-forty">
            <plusIcon/>
        </button>
    </div>
    <!-- button end  -->
<transition name="fade-scale">
         <div v-if="isAddserver" class="fixed w-full z-50 inset-0 bg-dark flex justify-center items-center">
        
        <div class="bg-forty/60 backdrop-blur-md w-86 h-96 p-6">
        <div class="w-full flex justify-between p-2">
            <div>
                <h1>Add Server</h1>
            </div>
            <div @click="addServerToggle" class="w-8 h-8 flex justify-center items-center cursor-pointer text-forty font-bold rounded-full bg-thirty">
                <h1>X</h1>
            </div>
        </div>
            <form action="">
                <div class="flex flex-col gap-1">
                    <label for="root">
                        root: 
                    </label>
                    <input type="text" placeholder="root user" class="p-2 outline-2 outline-primary rounded-lg bg-light" />
                </div>

                <div class="flex flex-col gap-1">
                    <label for="root">
                        ip: 
                    </label>
                    <input type="text" placeholder="server ip" class="p-2 outline-2 outline-primary rounded-lg bg-light" />
                </div>

                <div class="flex flex-col gap-1">
                    <label for="root">
                        port: 
                    </label>
                    <input type="text" placeholder="port" class="p-2 outline-2 outline-primary rounded-lg bg-light" />
                </div>
                <div class="flex justify-around my-5">
                    <button type="submit" class="p-2 w-20 bg-success flex justify-center items-center rounded-md hover:bg-forty cursor-pointer outline-2 outline-offset-2 outline-success/50 hover:outline-success active:bg-success/90 transition-all duration-300"> <plusIcon class="w-4 hover:rotate-90 h-4 fill-forty" /> </button>
                    <button @click="addServerToggle" type="button" class="p-2 w-20 bg-danger text-forty hover:text-danger font-bold flex justify-center items-center rounded-md hover:bg-forty cursor-pointer outline-2 outline-offset-2 outline-danger/50 hover:outline-danger active:bg-danger/90 transition-all duration-300">close</button>
                </div>
            </form>
        </div>
     </div>
</transition>
</template>


<style scoped>
.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: all 0.3s ease;
}
.fade-scale-enter-from,
.fade-scale-leave-to {
  opacity: 0;
  transform: scale(0.95);
}
.fade-scale-enter-to,
.fade-scale-leave-from {
  opacity: 1;
  transform: scale(1);
}
</style>