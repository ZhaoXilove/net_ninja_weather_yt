<template>
  <div>
    <Suspense>
      <AsyncCityViewVue />
      <template #fallback>
         <p>Loading..</p>
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityViewVue from "@/components/AsyncCityView.vue";
</script>
