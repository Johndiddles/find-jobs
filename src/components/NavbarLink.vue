<script setup>
import { defineProps } from "vue";
import { RouterLink, useRoute } from "vue-router";

defineProps({
  link: String,
  label: String,
});

const isActiveLink = (routePath) => {
  const route = useRoute();
  return route.path === routePath;
};
</script>

<template>
  <RouterLink
    :to="link"
    :class="`text-white  rounded-md px-3 py-2 ${
      isActiveLink(link) ? 'bg-green-900' : 'hover:bg-gray-900 hover:text-white'
    }`"
    >{{ label }}</RouterLink
  >
</template>
