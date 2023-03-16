<script setup>
// import { defineProps } from 'vue'

// const props = defineProps({
//   showModal: {
//     type: Boolean,
//     required: true
//   }
// })

// const closeModal = () => {
//   props.showModal = false
// }

</script>

<template>
    <div v-if="showModal" class="overlay"> 
      <div class="modal">
        <button @click="showModal = false" class="close"> 
          <img src="../assets/x.svg"/> 
        </button>
        <textarea name="note" id="note" cols="30" rows="10"></textarea>
        <button class="add-note">Add Note</button>
      </div>
    </div>
</template>

<style scoped>
.overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal{
    width: 750px;
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
    width: 100%;
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
    margin-left: 725px;
  }
</style>