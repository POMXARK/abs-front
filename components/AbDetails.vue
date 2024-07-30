<template>
  <div class="card">
    <div class="grid grid-cols-2 gap-10">
      <div class="p-7">
        <img :src="`${ab.photoLink}`" class="mx-auto my-7" />
      </div>
      <div class="p-7">
        <h2 class="text-4xl my-7">{{ ab.name }}</h2>
        <p class="text-xl my-7">Цена: {{ ab.price }} руб.</p>
        <h3 class="font-bold border-b-2 mb-4 pb-2">Описание:</h3>
        <p class="mb-7">{{ ab.fields.description }}</p>
        <div class="grid">
          <div v-for="photo in ab.fields.photos">
            <img :src="`${photo.link}`" class="" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  const { ab } = defineProps(['ab'])
</script>

<style scoped>
  img {
    max-width: 400px;
  }
</style>