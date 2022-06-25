<script setup lang="ts">
const {
  params: { slug }
} = useRoute()

const { data: article } = await useAsyncData(`article-${slug}`, () =>
  queryContent(`/articles/${slug}`).findOne()
)
const { data: allArticles } = await useAsyncData('article', () =>
  queryContent('/articles').find()
)

const articles = allArticles.value.map(article =>
  parseInt(article.title.split(':')[0])
)

const currentPath = ref(parseInt(article.value._path.split('/').pop()))
const firstItem = currentPath.value !== 1
const lastItem = currentPath.value !== articles[articles.length - 1]

useHead({
  title: article.value.title,
  meta: [{ name: 'description', content: `${article.value.description}` }]
})
</script>

<template>
  <main>
    <div class="content text-black dark:text-white leading-[2rem]">
      <section class="flex flex-row justify-between">
        <NuxtLink v-if="firstItem" :to="`/articles/00${currentPath - 1}`">
          <IconsArrowLeft />
        </NuxtLink>
        <h1 class="title" v-text="article.title" />
        <NuxtLink v-if="lastItem" :to="`/articles/00${currentPath + 1}`">
          <IconsArrowRight />
        </NuxtLink>
      </section>
      <ContentRenderer :value="article" class="main" />
    </div>
  </main>
</template>

<style scoped>
.main {
  @apply dark:text-white;
}
</style>
