<script setup>
import { HomeIcon } from '@heroicons/vue/20/solid';
import { useRoute } from 'vue-router';

const props = defineProps({
  homePath: null,
  items: Array,
});
const route = useRoute();

function checkIsActive(item) {
  if (!item.to) {
    return true;
  }

  if (item.paths.length < 2) {
    return item.id === route.name;
  }

  return item.paths.findIndex((itemPath) => itemPath.id === route.name) !== 1;
}
</script>

<template>
  <nav class="flex border-b border-gray-200 bg-white" aria-label="Breadcrumb">
    <ol
      role="list"
      class="mx-auto flex w-full max-w-screen-xl space-x-4 px-4 sm:px-6 lg:px-8"
    >
      <li class="flex">
        <div class="flex items-center">
          <router-link
            :to="props.homePath"
            class="text-gray-400 hover:text-gray-500"
          >
            <home-icon class="h-5 w-5 flex-shrink-0" />
          </router-link>
        </div>
      </li>
      <li v-for="item in items" :key="item.id" class="flex">
        <div class="flex items-center">
          <svg
            class="h-full w-6 flex-shrink-0 text-gray-200"
            viewBox="0 0 24 44"
            preserveAspectRatio="none"
            fill="currentColor"
            aria-hidden="true"
          >
            <path d="M.293 0l22 22-22 22h1.414l22-22-22-22H.293z" />
          </svg>
          <span
            v-if="checkIsActive(item)"
            class="ml-4 text-sm font-medium text-gray-700"
            >{{ item.name }}</span
          >
          <router-link
            v-else
            :to="item.to"
            class="ml-4 text-sm font-medium text-gray-500 hover:text-gray-700"
            >{{ item.name }}</router-link
          >
        </div>
      </li>
    </ol>
  </nav>
</template>
