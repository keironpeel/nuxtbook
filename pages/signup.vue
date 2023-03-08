<script setup lang="ts">
const email = ref("");
const password = ref("");

const client = useSupabaseClient();

async function register() {
  const { error } = await client.auth.signUp({
    email: email.value,
    password: password.value,
  });
  console.log("error", error);
}

const user = useSupabaseUser();

onMounted(() => {
  watchEffect(() => {
    if (user.value) {
      navigateTo("/");
    }
  });
});
</script>

<template>
  <h1>Login</h1>
  <form @submit.prevent="() => register()">
    <input
      type="email"
      placeholder="Email Address"
      class="input input-bordered w-full max-w-xs"
      v-model="email"
    />
    <input
      type="password"
      placeholder="Password"
      class="input input-bordered w-full max-w-xs"
      v-model="password"
    />
    <button class="btn btn-primary" type="submit">Signup</button>
  </form>
</template>
