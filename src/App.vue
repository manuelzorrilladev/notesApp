<script setup>
import { computed, ref, watch } from "vue";

import CardContainer from './components/CardContainer.vue'
import OverlayModal from './components/OverlayModal.vue'


let msg = "The note is too Short!!!"



const showModal = ref(false)

const notes = ref([])
const validateNote = ref(false)

function showModalHandler (){
  showModal.value = !showModal.value
}


function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%,1)"

}

const addNote = (note) => {

  if (note.length < 10 || note.length > 250) {

    if (note.length < 10) {
      msg = "The note is too Short!!!"
    } else {
      msg = "The note is too big!!!"
    }

    validateNote.value = true

  } else {

    notes.value.push({
      id: Math.floor(Math.random() * 10000),
      text: note,
      date: new Date(),
      backgroundColor: getRandomColor(),
      status:false
    })

    validateNote.value = false

  }

  showModal.value = false;
}


function changeNoteStatus (id){
  notes.value[id].status = !notes.value[id].status
}



</script>


<template>
  <main>
    <div class="warning" :class="validateNote ? 'show' : 'hidden'">
      <p>{{ msg }}</p>
    </div>

    <div v-if="showModal" class="overlay">

      <OverlayModal 
        
        @modal-handler="showModalHandler" 
        @add-note="addNote"
        :modal="showModal"
        />

    </div>

    <CardContainer
    @change-note-status="changeNoteStatus"
      @modal-handler="showModalHandler" 
      :modal="showModal"
      :notes="notes" 
      
      />

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

.warning {
  margin-top: 10px;
  position: absolute;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.warning p {
  width: 40%;
  text-align: center;
  padding: 20px;
  background: red;
}

.hidden {
  display: none;
}

.show {
  animation: warn 5s forwards;
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

@keyframes warn {
  0% {
    opacity: 1;
  }

  50% {
    opacity: 1;
  }

  100% {
    opacity: 0;
  }
}
</style>