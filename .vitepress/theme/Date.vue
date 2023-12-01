<script setup lang="ts">
import type { Post } from './posts.data.ts'
import { useData, useRoute } from 'vitepress'
const route = useRoute()
const props = defineProps<{ date: Post['date'] }>()

function getDateTime() {
  if (!props.date) console.log(route.path)
  return new Date(props.date.time).toISOString()
}
</script>

<template>
  <dl>
    <dt class="sr-only">Published on</dt>
    <dd class="text-base leading-6 font-medium text-gray-500 dark:text-gray-300">
      <time :datetime="getDateTime()">{{ date.string }}</time>
    </dd>
  </dl>
</template>