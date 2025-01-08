<script setup lang="ts">
import moment from 'moment';

import { computed } from 'vue';

const props = defineProps<{
    currentWeather: any;
}>()

const forecastWeather = computed(() => props.currentWeather.forecast.forecastday[0].hour)

</script>

<template>
    <div class="main_card">
        <h3>Current temperature: {{ Math.floor(props.currentWeather.current.temp_c) }}°C / {{
            props.currentWeather.current.temp_f
        }}°F</h3>
        <h2>Forecast for {{ moment(Date.now()).format('DD.MM.YYYY') }}: </h2>
        <div class="forecast_card">
            <div class="hour_card" v-for="(hour, index) in forecastWeather" :key="index">
                <span>{{ moment(hour.time).format('hh:mm A') }}</span>
                <span>{{ Math.floor(hour.temp_c) }}°C</span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.main_card {
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.forecast_card {
    display: grid;
    grid-template-columns: repeat(6, 100px [col-start]);
    gap: 10px;
    font-size: 19px;
}

.hour_card {
    background-color: dimgray;
    display: flex;
    flex-direction: column;
    padding: 4px;
    height: 90px;
    justify-content: center;
    align-items: center;
    border-radius: 15px;
}
</style>
