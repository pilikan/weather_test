<script setup lang="ts">
import { ref } from "vue";
import CountryForm from "./components/CountryForm.vue"
import Weather from "./components/Weather.vue";

import axios from "axios";

const currentCountry = ref<any>({})
const isError = ref<boolean>(false);
const currentWeather = ref<any>({})

const searchCountry = async (country: string): Promise<void> => {
  isError.value = false;
  let { data } = await axios.get(`https://geocoding-api.open-meteo.com/v1/search?name=${country}&count=10&language=en&format=json`)
  if (data.results) {
    currentCountry.value = data.results[0];
    getWeather();
  } else {
    isError.value = true;
  }
}

const getWeather = async (): Promise<void> => {
  let { data } = await axios.get(`https://api.weatherapi.com/v1/forecast.json?key=834272dad1a942a4afd94714250801&q=${currentCountry.value.latitude},${currentCountry.value.longitude}&aqi=no`)
  currentWeather.value = data
}
</script>

<template>
  <h1>Weather</h1>
  <CountryForm @searchCountry="searchCountry" />
  <span v-if="isError" style="color: red">Error, try again</span>
  <Weather v-if="Object.keys(currentWeather).length > 0" :currentWeather=currentWeather></Weather>
</template>

<style scoped></style>

834272dad1a942a4afd94714250801