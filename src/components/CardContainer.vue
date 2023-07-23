<script setup>
import { ref, watch } from 'vue';



const { modal, notes } = defineProps(['modal', 'notes'])
console.log(notes);
const emit = defineEmits(['modal-handler', 'change-note-status'])

const navigation = ref(0)
const navigationHeader = ref('All')
const allNotes = ref(notes)

const emitModalHandler = (modal) => {
    emit('modal-handler', modal)
}

const emitNoteStatus = (id) => {
    emit('change-note-status', id)
    navigation.value == navigation.value
}
function changeNavigation(input) {
    navigation.value = input
    if (input == 0) {
        navigationHeader.value = 'All'
    } else if (input == 1) {
        navigationHeader.value = 'Completed'
    } else {
        navigationHeader.value = 'Pending'

    }



}


watch(navigation, () => {
    if (navigation.value == 1) {
        allNotes.value = notes.filter(n => n.status == true)
    } else if (navigation.value == 2) {

        allNotes.value = notes.filter(n => n.status == false)
    } else {
        allNotes.value = notes
    }
})


</script>

<template>
    <div class="container">
        <header>
            <h1>Notes </h1>
            <button @click="emitModalHandler(modal)">+</button>
        </header>
        <h2 class="title">{{ navigationHeader }}</h2>
        <div class="content-container">
            <div v-if="allNotes.length > 0" class="cards-container">
                <div class="card" v-for="(note, index) in allNotes" :key="note.id"
                    :style="{ backgroundColor: note.backgroundColor }">

                    <p class="main-text">{{ note.text }}</p>
                    <div class="check">
                        <p class="date">{{ note.date.toLocaleDateString("es") }}</p>
                        <div class="check">
                            <label v-if="note.status == true" for="status">Completed:</label>
                            <label v-else for="status">Pending:</label>
                            <input type="checkbox" name="status" @change="emitNoteStatus(index)">
                        </div>
                    </div>
                </div>
            </div>

            <div v-else> There´s no notes :/</div>

            <div class="status-container">
                <h2 class="status-item" @click="changeNavigation(0)">All</h2>

                <h2 class="status-item" @click="changeNavigation(1)">Completed</h2>

                <h2 class="status-item" @click="changeNavigation(2)">Pending</h2>

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

.title {
    margin-bottom: 20px;
}

.content-container {
    display: flex;
    justify-content: space-between;
}

.cards-container {
    width: 85%;
    display: grid;
    grid-template-columns: repeat(auto-fit, 200px);

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

.status-item {
    cursor: pointer;
    padding: 5px 10px;
}

.status-item:hover,
.active {
    background-color: #c3c3c3;

}
</style>