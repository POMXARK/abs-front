<script setup>
// import GuestLayout from '@/Layouts/GuestLayout.vue';
// import InputError from '@/Components/InputError.vue';
// import InputLabel from '@/Components/InputLabel.vue';
// import PrimaryButton from '@/Components/PrimaryButton.vue';
// import TextInput from '@/Components/TextInput.vue';
// import { Head, Link, useForm } from '@inertiajs/vue3';

// const form = useForm({
//   name: '',
//   email: '',
//   password: '',
//   password_confirmation: '',
// });

const submit = async () => {
  console.log('Register')
  console.log(name.value)

  const {user, token} = (await $fetch('http://127.0.0.1/api/v1/register', {
    method: 'POST',
    body: JSON.stringify({
      name: name.value,
      email: email.value,
      password: password.value,
      passwordConfirmation: passwordConfirmation.value,
    }),
    headers: {"Content-Type": "application/json"}
  }))

  console.log('user:', user)
  console.log('token:', token)
};

const name = defineModel('name')
const email = defineModel('email')
const password = defineModel('password')
const passwordConfirmation = defineModel('passwordConfirmation')

</script>

<template>
  <GuestLayout>
    <Head title="Register" />

    <form @submit.prevent.stop="submit">
      <div>
        <InputLabel for="name" value="Name" />

        <TextInput
            id="name"
            type="text"
            class="mt-1 block w-full"
            v-model="name"
            required
            autofocus
            autocomplete="name"
        />
      </div>

      <div class="mt-4">
        <InputLabel for="email" value="Email" />

        <TextInput
            id="email"
            type="email"
            class="mt-1 block w-full"
            v-model="email"
            required
            autocomplete="username"
        />
      </div>

      <div class="mt-4">
        <InputLabel for="password" value="Password" />

        <TextInput
            id="password"
            type="password"
            class="mt-1 block w-full"
            v-model="password"
            required
            autocomplete="new-password"
        />
      </div>

      <div class="mt-4">
        <InputLabel for="password_confirmation" value="Confirm Password" />

        <TextInput
            id="password_confirmation"
            type="password"
            class="mt-1 block w-full"
            v-model="passwordConfirmation"
            required
            autocomplete="new-password"
        />
      </div>

      <div class="flex items-center justify-end mt-4">
        <NuxtLink
            to="/login"
            class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
        >
          Already registered?
        </NuxtLink>

        <PrimaryButton class="ms-4">
          Register
        </PrimaryButton>
      </div>
    </form>
  </GuestLayout>
</template>

<style scoped>
input, textarea {
  border: 2px dotted;
}
</style>