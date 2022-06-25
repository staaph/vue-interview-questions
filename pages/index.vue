<script setup lang="ts">
const { data: articles } = await useAsyncData('articles', () =>
  queryContent('/articles').find()
)

const layout = ref('list')

useHead({
  title: 'Home'
})
</script>

<template>
  <main class="flex flex-col items-center justify-center content">
    <h1 class="title">VueJS interview questions</h1>
    <section
      class="flex flex-row justify-end w-full gap-2 mb-2 md:w-2/3 dark:text-white"
    >
      <button @click="layout = 'list'">
        <IconsList />
      </button>
      <button @click="layout = 'grid'">
        <IconsGrid />
      </button>
    </section>
    <section
      v-if="articles"
      class="w-full gap-5 md:w-2/3"
      :class="{
        'flex flex-col': layout == 'list',
        'grid grid-cols-2 lg:grid-cols-3': layout == 'grid'
      }"
    >
      <div v-for="(article, key) in articles" :key="article.id">
        <NuxtLink :to="article._path">
          <div class="card">
            <div
              class="text-3xl font-bold text-gray-400 dark:text-gray-400"
              v-text="'0' + (key + 1)"
            />
            <div class="flex flex-col">
              <p class="font-semibold text-black" v-text="article.title" />
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
