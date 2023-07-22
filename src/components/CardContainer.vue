<script setup>


const {modal,notes} = defineProps(['modal','notes'])
const emit = defineEmits(['modal-handler'])

const emitModalHandler = (modal)=>{
    emit('modal-handler',modal)
}

</script>

<template>
    <div class="container">
        <header>
            <h1>Notes </h1>
            <button @click="emitModalHandler(modal)">+</button>
        </header>

        <div class="cards-container">
            <div class="card" v-for="note in notes" :key="note.id" :style="{ backgroundColor: note.backgroundColor }">
    
                <p class="main-text">{{ note.text }}</p>
                <p class="date">{{ note.date.toLocaleDateString("es") }}</p>
                
            </div>
        </div>
    </div>
</template>

<style scoped>
.container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
}

header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 100%;
    color: white;
    font-size: 20px;
}

.cards-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, 150px);

    gap: 2.5rem;
}


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