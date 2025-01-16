<template>
    <div>
        <div class="top-row">
            <div class="weather">날씨</div>
            <div class="prefer">배경설정</div>
        </div>
        <div class="empty-space"></div>
        <div class="time-wrap">
            <h1>{{nowH}}</h1>
            <h1 class="colon">:</h1>
            <h1>{{nowM}}</h1>
        </div>
        <div class="main-ment">
            <h2>Find Your Way, {{ userName }}</h2>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const props = defineProps<{
    userName: string | null
}>()

const nowH = ref('00');
const nowM = ref('00');
const getNowTime = () => {
    const now = new Date();
    nowH.value = String(now.getHours()).padStart(2, '0');
    nowM.value = String(now.getMinutes()).padStart(2, '0');   
}
setInterval(getNowTime, 1000);
</script>

<style scoped>
</style>