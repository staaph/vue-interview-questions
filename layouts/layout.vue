<script setup lang="ts">
useHead({
  title: 'Vue interview questions',
  viewport: 'width=device-width, initial-scale=1, maximum-scale=1',
  charset: 'utf-8',
  meta: [
    { name: 'description', content: 'Common interview questions regarding Vue' }
  ]
})
</script>

<template>
  <main class="main">
    <Navbar />
    <slot />
  </main>
</template>

<style scoped>
.main {
  @apply min-h-screen;
}
</style>
