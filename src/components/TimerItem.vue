<script setup lang="ts">
interface Props {
  time: string,
  timeName: string
}

defineProps<Props>()
</script>

<template>
  <div>
    <p>{{time}}</p>
    <span>{{timeName}}</span>
  </div>
</template>

<style scoped>
  div {
    display: flex;
    min-width: 120px;
    margin: 0;
    padding: 10px 15px;
    border-radius: 8px;
    text-align: center;
    flex-direction: column;
    justify-content: center;
    gap: 8px;  
    background: #181818;
  }
  
  div span {
    font-weight: 600;
    letter-spacing: 2px;
    font-size: 16px;
  }

  p {
    margin: 0px;
    font-size: 45px;
    font-weight: 600;
  }
</style>
