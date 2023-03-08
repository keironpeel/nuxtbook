<script setup lang="ts">
const client = useSupabaseClient();
const user = useSupabaseUser();

async function logout() {
  const { error } = await client.auth.signOut();
  console.error(error);
  navigateTo("/login");
}
</script>

<template>
  <header class="navbar bg-base-100">
    <div class="flex-1">
      <a class="btn btn-ghost normal-case text-xl">NuxtBook</a>
    </div>
    <nav class="flex-none">
      <ul class="menu menu-horizontal px-1">
        <li><NuxtLink to="/">Home</NuxtLink></li>
        <li v-if="!user"><NuxtLink to="/login/">Login</NuxtLink></li>
        <li v-if="user" @click="() => logout()"><p>Logout</p></li>
      </ul>
    </nav>
  </header>
</template>
