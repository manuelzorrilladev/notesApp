<script setup>
const note = defineProps(['note'])
</script>

<template>
<div class="card" :key="note.id" :style="{ backgroundColor: note.backgroundColor }">
    
    <p class="main-text">{{ note.text }}</p>
    <p class="date">{{ note.date.toLocaleDateString("es") }}</p>
    
</div>
   
    
</template>

<style scoped>
.card {
    width: 150px;
    height: 150px;
    background-color: red;
    padding: 10px;
    border-radius: 20px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  
  }
  .card .main-text {
    width: 100%;
    word-wrap: break-word
  }
</style>