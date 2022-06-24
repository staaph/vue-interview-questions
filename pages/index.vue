<script setup lang="ts">
const { data: articles } = await useAsyncData('articles', () =>
  queryContent('/articles').find()
)
useHead({
  title: 'Home'
})
</script>

<template>
  <main class="flex flex-col items-center justify-center content">
    <h1 class="title">
      VueJS interview questions
    </h1>
    <section v-if="articles" class="flex flex-col w-full gap-5 md:w-2/3">
      <div v-for="(article, key) in articles" :key="article.id">
        <NuxtLink :to="article._path">
          <div class="card">
            <div
              class="text-3xl font-bold text-gray-400 dark:text-gray-400"
              v-text="'0' + (key + 1)"
            />
            <div class="flex flex-col">
              <p class="font-semibold" v-text="article.title" />
            </div>
          </div>
        </NuxtLink>
      </div>
    </section>
  </main>
</template>

<style scoped>
.card {
  @apply dark:text-black dark:hover:text-white flex flex-row gap-x-3 bg-gray-100 p-2 rounded hover:scale-[103%] hover:bg-gray-900/25 transition-all duration-500 items-center dark:hover:bg-gray-600/50;
}
</style>
