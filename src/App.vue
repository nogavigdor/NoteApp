<script setup>
import { ref } from 'vue'

const showModal = ref(false)
const newNote = ref('')
const notes = ref([])

function getColor() {
  return (
    'hsl(' +
    360 * Math.random() +
    ',' +
    (25 + 70 * Math.random()) +
    '%,' +
    (85 + 10 * Math.random()) +
    '%)'
  )
}

const addNote = () => {
  let noteObj = {
    text: newNote.value,
    date: new Date().toLocaleDateString(),
    color: getColor(),
    id: Math.floor(Math.random() * 1000000)
  }
  notes.value.push(noteObj)
  newNote.value = ''
  showModal.value = false
}
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" rows="30" cols="30"></textarea>
        <button @click="addNote" class="add">Add Note</button>
        <button @click="showModal = false" class="close">Close</button>
      </div>
    </div>

    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-containr">
        <div
          v-for="note in notes"
          class="card"
          :style="{ backgroundColor: note.color }"
          :key="note.id"
        >
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>
<style scoped>
main {
  width: 100vw;
  height: 100vh;
  color: #333;
  background-color: lavenderblush;
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
  font-size: 75px;
  font-weight: 700;
  margin-bottom: 20px;
}

header button {
  height: 50px;
  width: 50px;
  border: none;
  padding: none;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  color: white;
  border-radius: 100%;
  font-size: 20px;
}

.card {
  height: 225px;
  width: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}

.date {
  font-size: 14px;
  font-weight: 500;
}

.cards-containr {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  width: 100%;
  height: 100%;
  position: absolute;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  position: relative;
  background-color: white;
  width: 750px;
  height: 400px;
  max-height: 80vh;
  padding: 30px;
  border-radius: 30px;
  display: flex;
  flex-direction: column;
}

.modal .add,
.modal .close {
  width: 100%;
  border: none;
  padding: 10px 20px;
  font-size: 20px;
  margin-top: 15px;
  color: white;
  font-size: 20px;
  cursor: pointer;
}

.modal .add {
  background-color: purple;
}

.modal .close {
  background-color: rgb(174, 15, 15);
}
</style>
