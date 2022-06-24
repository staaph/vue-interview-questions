<script setup lang="ts">
const {
  params: { slug }
} = useRoute()

const { data: article } = await useAsyncData(`article-${slug}`, () =>
  queryContent(`/articles/${slug}`).findOne()
)

useHead({
  title: article.value.title,
  meta: [{ name: 'description', content: `${article.value.description}` }]
})
</script>

<template>
  <main class="flex items-center justify-center w-full">
    <div class="content text-black dark:text-white leading-[2rem]">
      <h1 class="title" v-text="article.title" />
      <ContentRenderer :value="article" class="main" />
    </div>
  </main>
</template>

<style scoped>
.main {
  @apply dark:text-white;
}
</style>
