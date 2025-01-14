<template>
  <div class="bg" :style="{ 'background-image': `url(${bgArr[randomNum]})` }"></div>
</template>

<script setup lang="ts">
// import { reactive } from 'vue';
import { ref } from 'vue'
import bg01 from '/bg/bg_Img_01.jpg'
import bg02 from '/bg/bg_Img_02.jpg'
import bg03 from '/bg/bg_Img_03.jpg'
import bg04 from '/bg/bg_Img_04.jpg'
import bg05 from '/bg/bg_Img_05.jpg'
import bg06 from '/bg/bg_Img_06.jpg'
import bg07 from '/bg/bg_Img_07.jpg'
import bg08 from '/bg/bg_Img_08.jpg'
import bg09 from '/bg/bg_Img_09.jpg'
import bg10 from '/bg/bg_Img_10.jpg'

const bgArr = [bg01, bg02, bg03, bg04, bg05, bg06, bg07, bg08, bg09, bg10]

const randomNum = ref(0)
const getRandomNum = () => (randomNum.value = Math.floor(Math.random() * 10))
getRandomNum()
// const timeUpdate = setInterval(getRandomNum, 36000);
</script>

<style scoped>
.bg {
  width: 100%;
  height: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  opacity: 0.8;
}
</style>
