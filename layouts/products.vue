<template>
  <div>
    <header class="shadow-sm bg-white">
      <nav class="container mx-auto p-4">
        <NuxtLink to="/abs" class="font-bold">Объявления</NuxtLink>
      </nav>
    </header>
    <div class="container mx-auto p-4">
      <slot />
    </div>
    <footer class="container mx-auto p-4 flex justify-between border-t-2">
      <ul class="flex gap-4">
        <li><NuxtLink to="/">Главная</NuxtLink></li>
        <li><NuxtLink to="/abs">Объявления</NuxtLink></li>
      </ul>
    </footer>
  </div>
</template>

<style scoped>
  .router-link-exact-active {
    color: #12b488;
  }
</style>
<script setup lang="ts">
</script>