<script setup lang="ts">
import { useData, useRoute } from 'vitepress'
import Home from './Home.vue'
import Page from './Page.vue'
import Article from './Article.vue'
import NotFound from './NotFound.vue'

const route = useRoute()
const { page, frontmatter } = useData()
</script>

<template>
  <div class="antialiased dark:bg-slate-900">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 xl:max-w-5xl xl:px-0">
      <nav class="flex space-x-6 items-center py-10 font-semibold">
        <a 
          href="/" 
          :class="[route.path == '/' ? 'text-gray-700' : 'text-gray-600']"
          class="text-lg hover:text-gray-700 dark:hover:text-gray-200">
          Home
        </a>
        <a
          href="/about.html"
          :class="[route.path == '/about.html' ? 'text-gray-700' : 'text-gray-600']"
          class="text-lg hover:text-gray-700 dark:hover:text-gray-200">
          About
        </a>
      </nav>
    </div>
    <main class="max-w-3xl mx-auto px-4 sm:px-6 xl:max-w-5xl xl:px-0">
      <Home v-if="frontmatter.index" />
      <Page v-else-if="frontmatter.page" />
      <NotFound v-else-if="page.isNotFound" />
      <Article v-else />
    </main>
  </div>
</template>