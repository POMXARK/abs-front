<script setup>
const name = defineModel('name')
const description = defineModel('description')
const photo1 = defineModel('photo1')
const photo2 = defineModel('photo2')
const photo3 = defineModel('photo3')
const price = defineModel('price')


const submit = async () => {
  const config = useRuntimeConfig()

  (await $fetch(config.public.apiBase + '/abs', {
    method: 'POST',
    body: JSON.stringify({
      name: name.value,
      description: description.value,
      photos: [photo1.value, photo2.value, photo3.value].filter(x=> x != null),
      price: price.value,
    }),
    headers: {"Content-Type": "application/json"}
  }))

  window.location.reload()
};

</script>

<template>
  <form @submit.prevent="submit">
    <div>
      <InputLabel for="name" value="Название" />

      <TextInput
          id="name"
          type="text"
          class="mt-1 block w-full"
          v-model="name"
          required
          autofocus
      />
    </div>

    <div>
      <InputLabel for="description" value="Описание" />

      <TextTextarea
          id="description"
          type="text"
          class="mt-1 block w-full"
          v-model="description"
          required
          autofocus
      />
    </div>

    <div>
      <InputLabel for="photos" value="Ссылки на фото" />

      <TextInput
          id="photo1"
          type="url"
          class="mt-1 block w-full"
          v-model="photo1"
          autofocus
      />
      <TextInput
          id="photo2"
          type="url"
          class="mt-1 block w-full"
          v-model="photo2"
          autofocus
      />
      <TextInput
          id="photo3"
          type="url"
          class="mt-1 block w-full"
          v-model="photo3"
          autofocus
      />
    </div>

    <div>
      <InputLabel for="price" value="Цена" />

      <TextInput
          id="price"
          type="number"
          class="mt-1 block w-full"
          v-model="price"
          required
          autofocus
      />
    </div>

    <div class="flex items-center justify-end mt-4">

      <PrimaryButton class="ms-4">Создать</PrimaryButton>
    </div>
  </form>
</template>

<style scoped>
input, textarea {
  border: 2px dotted;
}
</style>