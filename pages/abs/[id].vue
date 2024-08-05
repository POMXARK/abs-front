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
const config = useRuntimeConfig()
const { id } = useRoute().params

const uri = config.public.apiBase + '/abs/' + id + '?fields[]=description&fields[]=photos'

//  fetch the products
const { data: ab } = await useFetch(uri, { key: id })

if (!ab.value) {
  throw createError({ statusCode: 404, statusMessage: 'Product not found' })
}

definePageMeta({
  layout: "abs",
})
</script>