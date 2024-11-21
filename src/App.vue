<script setup>
  import { ref } from 'vue';
  const showModal = ref(false)
  const newNote = ref("")
  const notes = ref([]);

  function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }

  const addNote = () =>{
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    });
    showModal.value = false;
    newNote.value = ""
  }

</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div> 
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal=true">+</button>
      </header>
      <div class="card-container">
        <div v-for="note in notes" 
        :key="note.id"
        class="card" :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString(en-US) }}</p>
        </div>
      </div>
    </div>
  </main>
 
</template>



<style scoped>
  main{
    height: 10vh;
    width: 100vw;
  }
  .container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }
  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  h1{
    font-weight: bild;
    margin-bottom: 25px;
    font-size: 75px;
  }
  header button{
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
  .card{
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-left: 20px;
  }
  .date{
    font-size: 12.5px;
    font-weight: bold;
  }
  .card-container{
    display: flex;
    flex-wrap: wrap;
  }
  .overlay {
    position: fixed; /* Ensure it stays in one place while scrolling */
    top: 0;
    left: 0;
    width: 100vw; /* Full width */
    height: 100vh; /* Full height */
    background-color: rgba(0, 0, 0, 0.77); /* Semi-transparent background */
    z-index: 10; /* Ensure it is above other elements */
    display: flex; /* Flexbox for centering */
    align-items: center; /* Vertically center */
    justify-content: center; /* Horizontally center */
}

  .modal{
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }
  .modal .close{
    background-color: brown;
    margin-top: 7px;
  }
</style>