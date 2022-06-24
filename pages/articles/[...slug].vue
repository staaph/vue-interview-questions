<script setup lang="ts">
const {
  params: { slug }
} = useRoute()

const { data: article } = await useAsyncData(`article-${slug}`, () =>
  queryContent(`/articles/${slug}`).findOne()
)

const showContent = ref(false)

useHead({
  title: article.value.title,
  meta: [{ name: 'description', content: `${article.value.description}` }]
})
</script>

<template>
  <main>
    <div class="content text-black dark:text-white leading-[2rem]">
      <h1 class="title" v-text="article.title" />
      <input type="checkbox" @click="showContent = !showContent">
      <label class="ml-2"><span v-if="!showContent">show</span> <span v-else>hide</span> answer</label>
      <ContentRenderer v-if="showContent" :value="article" class="main" />
    </div>
  </main>
</template>

<style scoped>
.main {
  @apply dark:text-white;
}

</style>
