<script setup lang="ts">
import {ref} from 'vue';
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

let finalDate: number = new Date("April 8, 2024 02:30:00 UTC").getTime();

function calculateTimeLeft() {
  let now: number = new Date().getTime();

  let dateDiference = finalDate - now;

  let days = Math.floor(dateDiference / (1000 * 60 * 60 * 24));
  let hours = Math.floor((dateDiference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  let minutes = Math.floor((dateDiference % (1000 * 60 * 60)) / (1000 * 60));
  let seconds = Math.floor((dateDiference % (1000 * 60)) / 1000);

  counter.value = {
    days: days < 10 ? `0${days}` : `${days}`,
    hours: hours < 10 ? `0${hours}` : `${hours}`,
    minutes: minutes < 10 ? `0${minutes}` : `${minutes}`,
    seconds: seconds < 10 ? `0${seconds}` : `${seconds}`,
  }

  setTimeout(calculateTimeLeft, 1000);
}

calculateTimeLeft();
</script>

<template>
    <main>
        <h1><span>DiegPS</span> ban timer</h1>
        <article>
            <TimerItem timeName="Days" :time="counter.days"/>
            <TimerItem timeName="Hours" :time="counter.hours"/>
            <TimerItem timeName="Minutes" :time="counter.minutes"/>
            <TimerItem timeName="Seconds" :time="counter.seconds"/>
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
