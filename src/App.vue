<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
      <nav>
        <RouterLink to="/">Home</RouterLink>|
        <RouterLink to="/order">order</RouterLink>
      </nav>
  <RouterView />
</template>

