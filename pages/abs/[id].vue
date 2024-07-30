<template>
  <div>
    <Head>
      <Title>{{ ab.name }}</Title>
      <Meta name="description" :content="ab.description" />
    </Head>

    <AbDetails :ab="ab" />
  </div>
</template>

<script setup>
const { id } = useRoute().params
const uri = 'http://127.0.0.1/api/v1/abs/' + id + '?fields[]=description&fields[]=photos'

//  fetch the products
const { data: ab } = await useFetch(uri, { key: id })

console.log(ab)

if (!ab.value) {
  throw createError({ statusCode: 404, statusMessage: 'Product not found' })
}

definePageMeta({
  layout: "products",
})
</script>