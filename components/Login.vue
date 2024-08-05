<script setup>

const email = defineModel('email')
const password = defineModel('password')
const remember = defineModel('remember')

const submit = async () => {
  console.log('Login')
  console.log(name.value)

  const {user, token} = (await $fetch('http://127.0.0.1/api/v1/login', {
    method: 'POST',
    body: JSON.stringify({
      email: email.value,
      password: password.value,
    }),
    headers: {"Content-Type": "application/json"}
  }))

  console.log('user:', user)
  console.log('token:', token)
};
</script>

<template>
    <GuestLayout>
        <Head title="Log in" />

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    class="mt-1 block w-full"
                    v-model="email"
                    required
                    autofocus
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
                    autocomplete="current-password"
                />
            </div>

            <div class="block mt-4">
                <label class="flex items-center">
                    <Checkbox name="remember" v-model:checked="remember" />
                    <span class="ms-2 text-sm text-gray-600">Remember me</span>
                </label>
            </div>

            <div class="flex items-center justify-end mt-4">
              <NuxtLink
                  to="/"
                  class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
              >
                not registered?
              </NuxtLink>

                <PrimaryButton class="ms-4">
                    Log in
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