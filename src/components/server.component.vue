<script setup>
import {ref} from "vue";
// components
import addServerComponent from "./addServer.component.vue";
// icons 
import serverIcon from "./icons/server.icon.vue"
import rightIcon from "./icons/right.icon.vue"
import settingIcon from "./icons/setting.icon.vue"
import trashIcon from "./icons/trash.icon.vue"
const isSetting = ref(true);


const servers = ref([
    {id: "76sdas7d6sasd", root: "admin", serverIp: "127.23.12.33", isActive: false},
    {id: "3h4ncxiu84755", root: "admin", serverIp: "127.33.33.33", isActive: false},
    {id: "asjv9d0w9vcbv", root: "admin", serverIp: "127.112.11.11", isActive: false},
    {id: "bv4r5f8hb004i", root: "admin", serverIp: "127.87.44.55", isActive: false},
    {id: "ds5239fb9b8ds", root: "admin", serverIp: "127.02.02.11", isActive: false},
    {id: "343jfb8s932jr", root: "admin", serverIp: "127.9.00.12", isActive: false},
])

const activeId = ref(null);
// controls
const sideSetting = () => {
    isSetting.value = !isSetting.value
}
const isActive = ref(false)

const toggleActive = (id) => {
  const server = servers.value.find(s => s.id === id)
  if(server) server.isActive = !server.isActive
}
</script>
<template>
  <addServerComponent/>
    <div class="w-full p-2 grid lg:grid-cols-3 md:grid-cols-2 sm:grid-cols-1 place-items-center gap-2">
        <!-- server start  -->
        <div v-for="(server, index) in servers" :key="index" class="w-full h-auto p-2 m-2 bg-forty/20 backdrop-blur-md border-2 rounded-xl drop-shadow-2xl shadow-md border-thirty">
            <!-- server status  -->
             <div class="w-full grid grid-cols-2 grid-flow-row">
                
                <div class="flex justify-center items-center">
                    <h1 class="text-md text-forty font-bold">
                        root@{{ server.serverIp }}
                    </h1>
                </div>
                <div class="flex items-center justify-center gap-2">
                    <serverIcon
                    :class="[
    'w-8 h-8 p-1 transition-all duration-300',
    server.isActive ? 'fill-success bg-success/30 ' : 'fill-danger bg-danger/30'
  ]"/>
                    <div 
                    :class="[
      'flex justify-center items-center gap-1 font-bold transition-all duration-300',
      server.isActive ? 'text-success' : 'text-danger'
      ]">
                        <h1>active</h1>
                        
                        <span class="relative flex size-3 bottom-1">  <span 
                            :class="[
      'absolute inline-flex h-full w-full animate-ping rounded-full opacity-75 transition-all duration-300',
      server.isActive ? 'bg-success' : 'bg-danger'
      ]"></span>  <span
                        :class="[
      'relative inline-flex size-3 rounded-full transition-all duration-300',
      server.isActive ? 'bg-success' : 'bg-danger'
      ]"></span></span>
                    </div>
                </div>
                <div class="flex justify-start items-center">
                    <ul>
                      <li class="text-forty">id: <span class="text-thirty font-bold">{{ server.id }}</span></li>
                      <li class="text-forty">root user: <span class="text-thirty font-bold">{{ server.root }}</span></li>
                    </ul>
                </div>
             </div>
             <div class="w-full">
             </div>
             <div class="w-full flex justify-between relative">
                <button
    @click="toggleActive(server.id)"
  :class="[
    'w-28 h-8 rounded-lg font-bold transition-all duration-300',
    server.isActive
      ? 'flex justify-center items-center text-forty rounded-xl m-2 font-bold hover:bg-success/20 bg-success/80 cursor-pointer transition-all outline-2 outline-offset-2 outline-success/50 active:bg-success/90'
      : 'flex justify-center items-center text-forty rounded-xl m-2 font-bold hover:bg-danger/20 text-danger bg-danger/80 cursor-pointer transition-all outline-2 outline-offset-2 outline-danger/50 active:bg-danger/90'
  ]"
  >
    {{ isActive ? 'Aktif' : 'Deaktif' }}
  </button>
  <button
  @click="sideSetting"
    class="group text-forty select-none p-2 px-2 bg-second cursor-pointer fill-forty hover:fill-dark rounded-lg flex items-center gap-2 font-bold transition-all duration-300 ease-in-out hover:bg-forty hover:text-dark hover:shadow-lg hover:scale-105"
  >
    <settingIcon class="w-5 h-5 transition-transform duration-300 group-hover:rotate-90"/>
    <h1>Settings</h1>
  </button>
</div>
        </div>
        <!-- server end  -->

         
         
    </div>

   <!-- sidebar start       -->
   <transition name="slide"> 
   <div class="w-1/2 h-screen  fixed select-none top-0 right-0 bg-primary/60 backdrop-blur-md border-l-2 border-forty" v-if="!isSetting">
        <div class="w-full">
            <div @click="sideSetting" class="flex m-2 hover:rotate-180 hover:bg-primary hover:text-forty transition-all items-center justify-center p-2 w-8 h-8 rounded-full bg-primary cursor-pointer">
                <h1 class="text-forty font-bold">X</h1>
            </div>
            <div class="w-full flex justify-center items-center absolute bottom-0">
                <ul class="w-full flex justify-center items-center">
                    <li @click="sideSetting"  class="w-full h-12 flex justify-center items-center text-forty rounded-xl m-2 font-bold hover:bg-danger/10 text-danger bg-danger/80 cursor-pointer transition-all outline-2 outline-offset-2 outline-danger/50 active:bg-danger/90">
                        <trashIcon class="fill-forty w-4 h-4"/>
                        remove
                    </li>
                </ul>
            </div>
        </div>
    </div>
</transition>
    <!-- sidebar end  -->
</template>



<style scoped>
/* Slide-in transition */
.slide-enter-from {
  transform: translateX(100%);
}
.slide-enter-active {
  transition: transform 0.3s ease;
}
.slide-enter-to {
  transform: translateX(0);
}

.slide-leave-from {
  transform: translateX(0);
}
.slide-leave-active {
  transition: transform 0.3s ease;
}
.slide-leave-to {
  transform: translateX(100%);
}
</style>