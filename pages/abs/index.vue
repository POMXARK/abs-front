<template>
  <div>
    <div class="grid grid-cols-4 gap-5">
      <div v-for="ab in abs">
        <AbCard :ab="ab" />
      </div>
    </div>
  </div>
</template>

<script setup>
//  fetch the products
const { data } = (await useFetch('http://127.0.0.1/api/v1/abs'))

console.log(data._rawValue.data)

const abs = data._rawValue.data

definePageMeta({
  layout: "products",
})

</script>