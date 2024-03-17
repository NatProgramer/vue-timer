<script setup lang="ts">
import { ref } from 'vue';

  interface Time {
    seconds: string,
    minutes: string,
    hours: string,
    days: string
  }

  let counter = ref<Time>({
    seconds: "00",
    minutes: "00",
    hours: "00",
    days: "00"
  });
  
  let actualDate = new Date();
  let finalDate = new Date(2024, 3, 7);
  
  const calculateSeconds = () => {
    let now = new Date();
    let seconds = `${Math.floor(59 - now.getSeconds())}`;

    if (parseInt(seconds) < 10) {
      seconds = `0${seconds}`
    }
    
    return calculateMinutes(seconds)
  }

  const calculateMinutes = (seconds: string) => {
    let now = new Date();
    
    let finalMinute = new Date();
    finalMinute.setHours(now.getHours(), 59, 59, 999);

    let minutes = `${Math.floor((finalMinute.getTime() - now.getTime()) / 1000 / 60)}`; 

    if (parseInt(minutes) < 10) {
      minutes = `0${minutes}`
    }

    return calculateHours(seconds, minutes)
  };

  const calculateHours = (seconds: string, minutes: string) => {
    let now = new Date();
  
    let finalHour = new Date();
    finalHour.setHours(23, 59, 59, 999);

    let hours = `${Math.floor((finalHour.getTime() - now.getTime()) / 1000 / 60 / 60)}`;

    if (parseInt(hours) < 10) {
      hours = `0${hours}`
    }

    return calculateDays(seconds, minutes, hours)
  }
  
  let calculateDays = (seconds: string, minutes: string, hours: string) => {
    let dateDiference = finalDate.getTime() - actualDate.getTime();
    let days = `${Math.floor(dateDiference / 1000 / 60 / 60 / 24)}`;

    if (parseInt(days) < 10) {
      days = `0${days}`
    }

    counter.value = {
      seconds,
      minutes,
      hours,
      days,
    }
  }

  setInterval(() => {
    calculateSeconds()
  }, 1000)
</script>

<template>
  <main>
    <h1><span>diegPS</span> ban counter</h1>
    <article>
      <p>{{counter.days}}</p>
      <p>{{counter.hours}}</p>
      <p>{{counter.minutes}}</p>
      <p>{{counter.seconds}}</p>
  </article>
  </main>
</template>

<style scoped>
  h1 {
    font-size: 40px;
    letter-spacing: 10px;
  }
  main {
    display: flex;
    height: 100%;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  main h1 {
    margin-bottom: 10px;
  }

  article {
    display: flex;
    gap: 15px;
  }

  article p {
    margin: 0;
    padding: 10px 15px;
    border-radius: 8px;
    font-size: 45px;
    font-weight: 600;
    background: #181818;
  }
</style>
