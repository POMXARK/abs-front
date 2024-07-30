<template>
  <div>
    <header class="shadow-sm bg-white">
      <nav class="container mx-auto p-4 flex justify-between">
        <NuxtLink to="/" class="font-bold">ABS</NuxtLink>
        <ul class="flex gap-4">
          <li><NuxtLink to="/">Главная</NuxtLink></li>
          <li><NuxtLink to="/abs" class="btn">Объявления</NuxtLink></li>
        </ul>
      </nav>
    </header>
    <div class="container mx-auto p-4">
      <slot />
    </div>
  </div>
</template>

<style scoped>
  .router-link-exact-active {
    color: #12b488;
  }
</style>