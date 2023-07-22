<script setup>
import { ref } from 'vue';

const {modal} = defineProps(['modal'])
const emit = defineEmits(['modal-handler','add-note'])



const newNote = ref("")


const emitModalHandler = (modal)=>{
    emit('modal-handler',modal)
}

const emitAddNote = (note)=>{
    emit('add-note',note)
}


</script>

<template>
    <div class="modal">

        <div class="upper">
            <h2>Notes must be at least 10 characters long</h2>
            <button class="close" @click="emitModalHandler(modal)">X</button>
        </div>

        <div class="input">
            <textarea v-model="newNote" name="notes" id="notes" cols="30" rows="10"
                placeholder="Write your note..."></textarea>
        </div>

        <button class="add" @click="emitAddNote(newNote)">Add Note</button>

    </div>
</template>

<style scoped>


.modal {
    width: 80vw;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: end;
}

.modal .upper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
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


</style>