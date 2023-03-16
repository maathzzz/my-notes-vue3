<script setup>
import { ref, onMounted } from 'vue';

// boolean 
const showModal = ref(false);
const newNote = ref("");
const notes = ref(JSON.parse(localStorage.getItem('notes') || '[]'));

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote = () => {
  const newNoteObj = {
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date().toLocaleString('pt-BR'),
    backgroundColor: getRandomColor()
  };
  notes.value.push(newNoteObj);
  showModal.value = false;
  newNote.value = "";
  // adding LocalStorage
  localStorage.setItem('notes', JSON.stringify(notes.value));
}

const deleteNote = (id) => {
  notes.value = notes.value.filter(note => note.id !== id);
  //adding LocalStorage
  localStorage.setItem('notes', JSON.stringify(notes.value));
}

onMounted(() => {
  const storedNotes = JSON.parse(localStorage.getItem('notes') || '[]');
  notes.value = storedNotes;
});
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay"> 
      <div class="modal">
        <button @click="showModal = false" class="close"> 
          <img src="./assets/x.svg"/> 
        </button>
        <textarea v-model="newNote" name="note" id="note" placeholder="Write here..." cols="30" rows="10"></textarea>
        <button class="add-note" @click="addNote">Add Note</button>
      </div>
    </div>

      <div class="container">
        <header>
          <h1> MyNotes </h1>
          <button @click="showModal = true">+</button> 
        </header>
        <div class="cards-container">
          <div v-bind:key="note.id"  v-for="note in notes" class="card" :style="{backgroundColor: note.backgroundColor}">
            <p class="main-text"> {{ note.text }} </p>
            <div class="card-footer">
            <p class="date">{{ note.date }}</p>
            <button class="delete-btn" @click="deleteNote(note.id)"> 
              <img src="./assets/trash.svg"/>
            </button>
            </div>
          </div>
        </div>
      </div>
  </main>
</template>

<style scoped>
  main {
    width: 100vw;
    height: 100vh;
  }
  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items:center
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 55px;
  }

  header button {
    border: none;
    padding: 10px;
    width: 60px;
    height: 60px;
    border-radius: 60px;
    background-color: rgb(21, 20, 20);
    font-size: 20px;
    color: white;
    transition: transform 300ms;
    cursor: pointer;
  }

  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }
  
  header button:active{
    transform: scale(0.88);
  }

  textarea {
    height: 200px;
    padding: 5px;
    font-size: 20px;
  }

  .main-text {
    line-height: 1.25;
    font-size: 15px;
    font-weight: bold;
  }

  .card{
    width: 200px;
    height: 200px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    overflow: hidden; /* add this property */
    word-wrap: break-word; /* add this property */
  }

  .delete-btn {
    background: none;
    border: none;
    cursor: pointer;
    transition: transform 300ms;
  }

  .delete-btn:active{
    transform: scale(0.88);
  }

  .date {
    font-size: 12px;
    margin-top: auto;
  }

  .card-footer {
    display: flex;
    justify-content: space-between;
  }

  .overlay{
    position: absolute;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0,0,0,0.77);
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal{
    width: 650px;
    background-color: white;
    border-radius: 10px;
    padding: 20px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .add-note{
    padding: 10px 20px;
    font-size: 20px;
    background-color:#2b2350;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 10px;
    border-radius: 5px;
  }

  .close {
    width: 30px;
    background: none;
    border:none;
    cursor: pointer;
    display: flex;
    margin-bottom: 10px;
    justify-content: end;
    margin-left: 625px;
  }
</style>