<script setup lang="ts">

import { ref } from 'vue'

const isModalOpen = ref(false)

</script>

<template>
  <div>
  <button class="btn" @click="isModalOpen = true"><slot name="openModalButtonName"></slot></button>
  <Teleport to="body">
    <Transition name="modal">
      <div class="modal-bg z-10" v-if="isModalOpen">
        <div class="modal">
          <button @click="isModalOpen = false" class="close-btn">x</button>
          <slot></slot>
        </div>
      </div>
    </Transition>
  </Teleport>
  </div>
</template>

<style scoped>
 .modal-bg {
   position: fixed;
   top: 0;
   left: 0;
   width: 100vw;
   height: 100vh;

   background-color: rgba(0, 0, 0, 0.5);

   display: flex;
   justify-content: center;
   align-items: center;
 }

 .modal {
   position: relative;

   background: white;
   padding: 50px 100px;
   border-radius: 5px;
   box-shadow: 0 10px 5px 2px rgba(0, 0, 0, 0.1);
 }

 .modal .close-btn {
   position: absolute;
   top: 10px;
   right: 10px;

   background: none;
   border: none;
   cursor: pointer;
 }

 .modal-enter-active,
 .modal-leave-active {
   transition: all .25s ease;
 }

 .modal-enter-from,
 .modal-leave-to {
   opacity: 0;
   transform: scale(1,1);
 }
</style>