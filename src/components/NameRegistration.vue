<template>
  <div class="first-view">
    <img src="@/assets/images/logo-white.svg" alt="logo" class="logo" />
    <div class="greeting-name">
      <h2>Hello!! What's your name?</h2>
      <input
        type="text"
        v-model.trim="userName"
        @keyup.enter="checkName"
        minlength="2"
        maxlength="30"
        autocomplete="off"
      />
      <h4>Please enter your first name or the name you prefer to be called.</h4>
      <button type="submit" @click="checkName">
        <span>Continue</span>
        <img src="@/assets/images/arrow-right.svg" alt="arrow" class="arrow" />
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const userName = ref('')

const checkName = () => {
  if (userName.value?.length < 2) {
    alert('두 글자 이상 입력해주세요')
  } else {
    goDashboard()
  }
}

const goDashboard = () => {
  emit('checHaskName', userName.value)
}

const emit = defineEmits<{
  checHaskName: [value: string]
}>()
</script>

<style scoped>
.first-view {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.logo {
  width: 80px;
  position: absolute;
  top: 5vh;
  left: calc(50% - 40px);
}
.greeting-name {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 35vh;
  margin-bottom: 20vh;
  padding: 10px 20px;
}
h2 {
  font-weight: 600;
}
input {
  margin-top: 40px;
  width: 660px;
  max-width: 660px;
}
h4 {
  font-size: 1.6rem;
  margin-top: 30px;
  letter-spacing: 0;
}
button {
  margin-top: 60px;
  padding: 10px 24px;
  border-radius: 30px;
  border: 2px white solid;
  background: rgba(0, 0, 0, 0.12);
  color: white;
  min-width: 40px;
  min-height: 30px;
  font-size: 1.6rem;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: background-color 0.2s ease;
}
button:hover {
  background: none;
}
button .arrow {
  margin-left: 6px;
  height: 16px;
  width: 20px;
}
</style>
