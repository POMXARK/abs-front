<template>
  <div class="card text-center">
    <img :src="`${ab.photoLink}`" class="thumb" />
    <p class="font-bold text-gray-500 m-4 truncate">{{ ab.name }}</p>
    <p class="font-bold text-gray-500 m-4 truncate">{{ ab.price }} руб.</p>
    <NuxtLink :to="`/abs/${ab.id}`">
      <p class="btn my-4">Посмотреть</p>
    </NuxtLink>
  </div>
</template>

<script setup>
  const { ab } = defineProps(['ab'])
</script>

<style scoped>
  .thumb {
    max-height: 120px;
    max-width: 70%;
    margin: 0 auto;
  }
</style>