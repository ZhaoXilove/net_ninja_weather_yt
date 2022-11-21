<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input
        type="text"
        v-model="searchQuery"
        @input="getSearchResults"
        placeholder="搜素一个城市或省"
        class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]"
      />
      <ul
        class="absolute bg-weather-secondary text-white w-full shadow-md py-2 px-1 top-[66px]"
        v-if="mapGaodeSearchResults.arr.lives"
        >
        <li
          class="py-2 cursor-pointer"
          :key="searchResult.adcode"
          v-for="searchResult in mapGaodeSearchResults.arr.lives"
        >
          {{ searchResult.province }}-{{ searchResult.city }}
        </li>
      </ul>
    </div>
  </main>
</template>

<script setup>
import { ref, reactive } from "vue";
import axios from "axios";
const KEY = ref("0bfebabfb6addc48914d7d6785d5298c");
const searchQuery = ref("");
const queryTimeout = ref(null);
const mapGaodeSearchResults = reactive({ arr: [] });
const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      const result = await axios.get(
        `https://restapi.amap.com/v3/weather/weatherInfo?key=${KEY.value}&city=${searchQuery.value}`
      );
      mapGaodeSearchResults.arr = result.data;
      console.log(mapGaodeSearchResults.arr);
      return;
    }
    mapGaodeSearchResults.arr = [];
  }, 300);
};
</script>

<style lang="scss" scoped></style>
