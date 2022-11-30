<template>
  <div class="flex flex-col flex-1 items-center">
    <div
      v-if="route.params.city"
      class="text-white p-4 bg-weather-secondary w-full text-center"
    >
      请打开视图点击+
    </div>
    <!-- Weather Overview -->
    <div class="flex flex-col items-center text-white py-12">
      <h1 class="text-4xl mb-20">{{ route.params.city }}</h1>
      <i class="fa-sharp fa-solid fa-snowflake text-8xl"></i>
      <p class="text-6xl mt-2 mb-8">{{ `${pageData.arr.temperature}°` }}</p>
      <p class="text-lg mt-6">{{ pageData.arr.weather }}</p>
      <p class="text-sm mt-6">{{ pageData.arr.reporttime }}</p>
      <p class="text-sm">{{ `湿度: ${pageData.arr.humidity}` }}</p>
      <p class="text-sm mb-6">{{ `风向: ${pageData.arr.windpower}级` }}</p>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { onMounted, ref, reactive } from "vue";
import { useRoute } from "vue-router";
const route = useRoute();
const KEY = ref("0bfebabfb6addc48914d7d6785d5298c");
const pageData = reactive({ arr: {} });
const getWeatherData = async (city) => {
  try {
    const weatherData = await axios.get(
      `https://restapi.amap.com/v3/weather/weatherInfo?key=${KEY.value}&city=${city}`
    );
    pageData.arr = weatherData.data.lives[0];
    console.log(pageData.arr.reporttime);
  } catch (err) {}
};
onMounted(() => {
  const { city } = route.params;
  getWeatherData(city);
});
</script>
