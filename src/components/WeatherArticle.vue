<template>
  <article class="weather-article">
    <div v-if="!isGetPositionFail && !isWeatherInfoLoaded" class="loading">
      <img src="/src/assets/images/spinner.svg" alt="loading" class="loading-i" />
    </div>
    <button v-else-if="isGetPositionFail" class="position-err" @click="getCurrentPosition">
      <!-- Not allowed location -->
      <img src="/src/assets/images/location.svg" alt="location" class="location-i" />
      <img src="/src/assets/images/refresh.svg" alt="refresh" class="refresh-i" />
    </button>
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
// const WEATHER_API_KEY = '27b2635bb20c1662a52dd2595a504721'
const KELVIN_TO_CELSIUS = 273.15

const getCurrentPosition = () => {
  isGetPositionFail.value = false
  console.log('getCurrentPosition', navigator)
  navigator.geolocation.getCurrentPosition(getPositionSuccess, getPositionFail)
}

const getPositionSuccess = (position: GeolocationPosition) => {
  const latitude = position.coords.latitude
  const longitude = position.coords.longitude
  console.log('getPositionSuccess!!!!!!!')

  getWeather(latitude, longitude)
}

const getPositionFail = () => {
  console.log('getPositionFailㅜㅜㅜㅜㅜ')
  isGetPositionFail.value = true
}

const getWeather = async (latitude: number, longitude: number) => {
  const url = `https://api.openweathermap.org/data/2.5/weather?lat=${latitude}&lon=${longitude}&appid=${import.meta.env.VITE_WEATHER_API_KEY}`
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
  getCurrentPosition()
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
.location-i {
  height: 20px;
  animation: normal4s linear 0s infinite alternate loading;
}
@keyframes loading {
  to {
    height: 20px;
    transform: rotate(1);
  }
}
.position-err-t {
  font-size: 1.4rem;
  font-weight: 500;
  /* letter-spacing: 1px; */
}
button.position-err {
  display: flex;
  align-items: end;
  filter: drop-shadow(1px 2px 6px rgba(0, 0, 0, 0.4));
}
button.position-err:hover .refresh-i {
  transform: rotate(45deg);
}
.position-err .location-i {
  width: 24px;
}
.position-err .refresh-i {
  width: 10px;
  transition: all 0.2s ease;
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
