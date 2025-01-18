<template>
  <article class="weather-article">
    <div v-if="!isGetPositionFail && !isWeatherInfoLoaded" class="loading">loading....</div>
    <h4 v-else-if="isGetPositionFail">지역 정보를 가져올수 없습니다</h4>
    <div v-else class="weather-info">
      <div class="weather-top">
        <img class="weather-i" :src="weather_icon_url" :alt="weather_text" />
        <span class="weather-temp">{{ weather_temperature }}</span>
      </div>
      <span class="weather-pos">{{ weather_position }}</span>
    </div>
  </article>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'

const isGetPositionFail = ref(false)
const isWeatherInfoLoaded = ref(false)
const weather_icon_url = ref('')
const weather_text = ref('')
const weather_temperature = ref('')
const weather_position = ref('')
const WEATHER_API_KEY = '27b2635bb20c1662a52dd2595a504721'
const KELVIN_TO_CELSIUS = 273.15

const getPositionSuccess = (position: GeolocationPosition) => {
  const latitude = position.coords.latitude
  const longitude = position.coords.longitude

  getWeather(latitude, longitude)
}

const getPositionFail = () => {
  isGetPositionFail.value = true
}

const getWeather = async (latitude: number, longitude: number) => {
  const url = `https://api.openweathermap.org/data/2.5/weather?lat=${latitude}&lon=${longitude}&appid=${WEATHER_API_KEY}`
  await fetch(url)
    .then((response) => {
      isWeatherInfoLoaded.value = true
      return response.json()
    })
    .then((json) => {
      weather_icon_url.value = `https://openweathermap.org/img/wn/${json.weather[0].icon}.png`
      weather_text.value = json.weather[0].main
      weather_temperature.value = `${(json.main.temp - KELVIN_TO_CELSIUS).toFixed(1)}º`
      weather_position.value = json.name
    })
    .catch((error) => {
      alert(error)
    })
}

onMounted(() => {
  navigator.geolocation.getCurrentPosition(getPositionSuccess, getPositionFail)
})
</script>

<style scoped>
.weather-article {
  width: 120px;
  height: 80px;
  padding: 5px 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.loading {
  font-size: 1.6rem;
  font-weight: 500;
  letter-spacing: 1px;
}
.weather-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.weather-top {
  width: 100%;
  display: flex;
  align-items: center;
}
.weather-top .weather-temp {
  font-size: 2.4rem;
  font-weight: 500;
  margin-left: 2px;
}
span {
  font-size: 1.4rem;
}
</style>
