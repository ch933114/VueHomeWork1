<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="">
    <nav class="flex justify-center gap-2 font-bold">
      <RouterLink to="/home" class="hover:text-accent1 active:text-black">Home</RouterLink>|
      <RouterLink to="/about" class="hover:text-accent1 active:text-black">About</RouterLink>|
      <RouterLink to="/" class="hover:text-accent1 active:text-black">第一周作業</RouterLink>
    </nav>
  </div>
  <RouterView />
</template>
