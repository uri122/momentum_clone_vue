<template>
  <div class="dashboard-view">
    <div class="top-row">
      <WeatherArticle />
      <div class="prefer">배경설정</div>
    </div>
    <div class="area-left"></div>
    <div class="area-center"></div>
    <div class="time-wrap">
      <h1>{{ nowH }}</h1>
      <h1 class="colon">:</h1>
      <h1>{{ nowM }}</h1>
    </div>
    <div class="main-ment">
      <h2>Find Your Way, {{ userName }}</h2>
    </div>
    <div class="area-right"></div>
    <div class="bottom-row"></div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import WeatherArticle from './WeatherArticle.vue'

defineProps<{
  userName: string | null
}>()

const nowH = ref('00')
const nowM = ref('00')
const getNowTime = () => {
  const now = new Date()
  nowH.value = String(now.getHours()).padStart(2, '0')
  nowM.value = String(now.getMinutes()).padStart(2, '0')
}
setInterval(getNowTime, 1000)
</script>

<style scoped>
.dashboard-view {
  width: 100%;
  height: 100%;
  /* display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center; */
  display: grid;
  grid-template-columns: var(--f20010c8) minmax(auto, 1fr) var(--f20010c8);
  grid-template-rows: var(--255f5fba) minmax(0, var(--28ea5c7c)) auto minmax(auto, 1fr) auto;
  overflow: hidden;
}
.top-row {
  grid-column: 1 / -1;
  grid-row: 1 / span 1;
  /* display: grid;
  grid-template-columns: minmax(auto, max-content) auto;
  grid-template-rows: auto auto; */
  display: flex;
  justify-content: space-between;
}
.area-left {
  /* grid-column: 1 / -1;
  grid-row: 2 / span 1;
  display: grid;
  grid-template-columns: minmax(auto, max-content) auto;
  grid-template-rows: auto auto; */
  grid-column: 1 / span 1;
  grid-row: 2 / span 3;
}
.area-center {
  grid-column: 2 / span 1;
  grid-row: 2 / span 1;
}
.time-wrap {
  grid-column: 2 / span 1;
  grid-row: 3 / span 1;
  display: flex;
  align-items: center;
}
.time-wrap h1 {
  color: white;
  font-size: 12rem;
  font-weight: 500;
  opacity: 1;
  transition: opacity ease-in-out 0.5s;
}
.time-wrap h1.colon {
  padding-bottom: 20px;
}
.main-ment {
  grid-column: 2 / span 1;
  grid-row: 4 / span 1;
  /* text-align: center;
  align-self: center;
    flex-direction: column;
    align-items: center; */
  margin-top: 40px;
  display: flex;
  /* align-items: center; */
}
input {
  width: 20vw;
}
.area-right {
  grid-column: -2 / span 1;
  grid-row: 2 / span 3;
}
.bottom-row {
  grid-column: 1 / -1;
  grid-row: 5 / span 1;
  align-items: end;
  display: grid;
    grid-template-columns: minmax(var(--02f62a0c),1fr) minmax(0,auto) minmax(var(--02f62a0c),1fr);
}
</style>
