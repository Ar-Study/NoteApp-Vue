<script setup>
import{ref} from 'vue';

const ShowForm = ref(false);
const newMemo = ref("");
const memos = ref([]);

function addMemo(){
  memos.value.push({
    id: Date.now(),
    memo: newMemo.value,
    date : new Date().toLocaleString("en-GB"),
    backgroundColor:getRandomColor(),
  })
  newMemo.value = "";
  ShowForm.value = false;
}
function getRandomColor(){
  return `#${Math.floor(Math.random() * 16777215).toString(16)}`
  }
</script>

<template>
{{ memos }}
  <main>
    <div class="container">
      <header>
        <h1 class="header-title">Note</h1> 
        <button @click="ShowForm=true" class="header-button">+</button>
      </header>
      <div class="card-container">
        <div v-for="memo in memos" :key="memo.id" class="card" :style="{ backgroundColor: memo.backgroundColor }">
          <p class="card-content">{{memo.memo}}</p>
          <p class="card-date">{{ memo.date }}</p>
        </div>
      </div>
    </div>
    <div v-if="ShowForm" class="form-overlay">
      <div class="form-box">
        {{ newMemo }}
        <button @click="ShowForm=false" class="form-close-btn">&times;</button>
        <textarea v-model="newMemo" name="memo" id="" cols="30" rows="10" class="form-textarea"></textarea>
        <button @click="addMemo" class="form-save-btn">Save</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
body {
  height: 100vh;
  width: 100vw;
  background: linear-gradient(135deg, #ff9a9e, #fad0c4);
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
}

.container {
  max-width: 600px;
  padding: 20px;
  margin: 0 auto;
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px solid #eee;
  padding-bottom: 10px;
}

.header-title {
  font-size: 24px;
  color: #333;
}

.header-button {
  background: #ff6b81;
  border: none;
  color: white;
  font-size: 20px;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  transition: 0.3s;
}

.header-button:hover {
  background: #ff4757;
}

.card-container {
  margin-top: 20px;
}

.card {
  background: #f8f9fa;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  font-size: 18px;
  color: #fff;
  margin-bottom: 10px;
}

/* Form Overlay Styling */
.form-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  /* visibility: hidden;
  opacity: 0;
  transition: visibility 0.3s, opacity 0.3s; */
}

.form-overlay.active {
  visibility: visible;
  opacity: 1;
}

.form-box {
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 350px;
}

.form-overlay .form-close-btn {
  align-self: flex-end;
  background: transparent;
  border: none;
  font-size: 30px;
  color: #333;
  cursor: pointer;
}

.form-overlay .form-textarea {
  width: 100%;
  height: 150px;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ddd;
  outline: none;
  font-size: 16px;
  resize: none;
}

.form-overlay .form-save-btn {
  margin-top: 10px;
  padding: 10px 20px;
  background: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  width: 100%;
}

.form-overlay .form-save-btn:hover {
  background: #218838;
}
</style>
