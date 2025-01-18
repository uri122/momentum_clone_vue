<template>
    <RandomBg />
    <main>
        <NameRegistration v-show="!userName" @chec-hask-name="checHaskName"/>
        <Dashboard v-show="userName" :user-name />
    </main>
</template>


<script setup lang="ts">
import { onBeforeMount, ref } from 'vue';
import RandomBg from './components/RandomBg.vue';
import NameRegistration from './components/NameRegistration.vue';
import Dashboard from './components/DashboardView.vue';

const userName = ref<string | null>(null);

const setUserName = () => { userName.value = sessionStorage.getItem("userName") };

const checHaskName = (name: string) => {
    sessionStorage.setItem("userName", name);
    setUserName();
}

onBeforeMount(() => setUserName());
</script>
