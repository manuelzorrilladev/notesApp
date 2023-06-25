<script lang="js" setup>
import { ref } from "vue";

const showModal = ref(false)
const newNote = ref("")
const notes = ref([])
const validateNote = ref(false)


let msg = "The note is too Short!!!"
function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%,1)"

}

const addNote = () => {

  if (newNote.value.length<10 || newNote.value.length >250) {

    if (newNote.value.length<10) {
      msg = "The note is too Short!!!"    
    } else {
      msg = "The note is too big!!!"        
    }
    
    validateNote.value = true 

  } else{

    notes.value.push({
      id: Math.floor(Math.random() * 10000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor(),
    })
    validateNote.value = false    
    
  }

  showModal.value = false;
  newNote.value = ""
}


</script>


<template>
  <main>
    <div class="warning" :class="validateNote ? 'show':'hidden'">
      <p>{{msg}}</p>
    </div>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <div class="upper">
          <h2>Notes must be at least 10 characters long</h2>
        <button class="close" @click="showModal = false">X</button>
        </div>
        <div class="input">
          <textarea v-model="newNote"  name="notes" id="notes" cols="30" rows="10"
            placeholder="Write your note..."></textarea>
        </div>
        <button class="add" @click="addNote">Add Note</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes </h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" class="card"
        :key="note.id"
        :style="{ backgroundColor: note.backgroundColor }">
          <p class="main-text">
            {{ note.text }}
            <!-- 2:34:35 -->

          </p>
          <p class="date">{{ note.date.toLocaleDateString("es") }}</p>
        </div>


      </div>
    </div>

  </main>
</template>
<style>
* {
  margin: 0px;
  padding: 0px;
  font-family: 'Roboto', sans-serif;
}
</style>
<style scoped>
main {
  height: 100vh;
}

.warning{
  margin-top: 10px;
  position: absolute;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}
.warning p{
  width: 40%;
  text-align: center;
  padding: 20px;
  background: red;
}
.hidden{
  display: none;
}

.show{
  animation: warn 5s forwards;
}

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

.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, 150px);

  gap: 2.5rem;
}

.card .main-text {
  width: 100%;
  word-wrap: break-word
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  width: 80vw;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: end;
}

.modal .input {
  width: 80vw;
  display: flex;
}

.modal .input textarea {

  width: 100%;
  height: 200px;
  resize: none;
  padding: 10px;
}

.modal .add {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;

}

.modal .close {
  background-color: red;
  border: none;
  padding: 5px;
  width: 35px;
  height: 35px;
  margin: 10px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 100%;
  color: white;
  font-size: 20px;
}
.upper{
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}
@keyframes warn {
  0%{
    opacity: 1;
  }
  50%{
    opacity: 1;
  }
  100%{
    opacity: 0;
  }
}

</style>