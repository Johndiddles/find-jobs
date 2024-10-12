<script setup>
import { RouterLink } from "vue-router";
import SingleJobListing from "@/components/SingleJobListing.vue";
import { ref, defineProps, onMounted } from "vue";

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
});

const jobs = ref([]);

onMounted(async () => {
  try {
    const response = await fetch("/api/jobs");
    const data = await response?.json();

    jobs.value = data;
  } catch (error) {
    console.log({ error });
  }
});
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:containter m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-[1500px] mx-auto">
      <SingleJobListing
        v-for="job in jobs.slice(0, limit || jobs.length)"
        :key="job.id"
        :job="job"
      />
    </div>
  </section>

  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>
