<template>
    <div class="card text-center">
      <img :src="`${photo.link}`" class="" />
    </div>
</template>

<script setup>
  const { photo } = defineProps(['photo'])
</script>

<style scoped>

</style>