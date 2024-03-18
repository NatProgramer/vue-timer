<script setup lang="ts">
import { ref } from 'vue';
import TimerItem from './components/TimerItem.vue';

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
    let now = new Date();
    let dateDiference = finalDate.getTime() - now.getTime();
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

  if (
      counter.value.days == "00" && 
      counter.value.hours == "00" && 
      counter.value.minutes == "00" && 
      counter.value.seconds == "00"
    ) { calculateSeconds() }

  setInterval(() => {
    calculateSeconds()
  }, 1000)
</script>

<template>
  <main>
    <h1><span>DiegPS</span> ban timer</h1>
    <article>
        <TimerItem timeName="Days":time="counter.days" />
        <TimerItem timeName="Hours" :time="counter.hours" />
        <TimerItem timeName="Minutes" :time="counter.minutes" />
        <TimerItem timeName="Seconds" :time="counter.seconds" />
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
</style>
