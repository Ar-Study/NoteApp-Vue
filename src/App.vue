<script setup>
import { ref } from "vue";

const ShowForm = ref(false);
const newMemo = ref("");
const memos = ref([]);
const errorMessage = ref("");

function addMemo() {
  if (!newMemo.value) {
    errorMessage.value = "Please enter a value";
    return;
  }
  memos.value.push({
    id: Date.now(),
    memo: newMemo.value,
    date: new Date().toLocaleString("en-GB"),
    backgroundColor: getRandomColor(),
  });
  newMemo.value = "";
  ShowForm.value = false;
  errorMessage.value = "";
}

function getRandomColor() {
  return `#${Math.floor(Math.random() * 16777215)
    .toString(16)
    .padStart(6, "0")}`;
}

function deleteMemo(id) {
  memos.value = memos.value.filter((memo) => memo.id !== id);
}
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1 class="header-title">Notes</h1>
        <button @click="ShowForm = true" class="header-button">+</button>
      </header>
      <div class="card-container">
        <div
          v-for="memo in memos"
          :key="memo.id"
          class="card"
          :style="{ backgroundColor: memo.backgroundColor }"
        >
          <p class="card-content">{{ memo.memo }}</p>
          <div class="card-footer">
            <p class="card-date">{{ memo.date }}</p>
            <button class="delete-btn" @click="deleteMemo(memo.id)">🗑️</button>
          </div>
        </div>
      </div>
    </div>

    <!-- Form Overlay -->
    <div v-if="ShowForm" class="form-overlay">
      <div class="form-box">
        <button @click="ShowForm = false" class="form-close-btn">
          &times;
        </button>
        <h2>Add Note</h2>
        <p class="error-message">{{ errorMessage }}</p>
        <textarea
          v-model="newMemo"
          placeholder="Write your note here..."
          class="form-textarea"
        ></textarea>
        <button @click="addMemo" class="form-save-btn">Save</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
/* General Layout */
body {
  height: 100vh;
  width: 100vw;
  background: linear-gradient(135deg, #ffdde1, #ee9ca7);
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: "Poppins", sans-serif;
}

/* Main Container */
.container {
  max-width: 500px;
  padding: 20px;
  background: white;
  border-radius: 12px;
  margin: 0 auto;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
}

/* Header */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px solid #eee;
  padding-bottom: 10px;
}

.header-title {
  font-size: 24px;
  font-weight: bold;
  color: #333;
}

.header-button {
  background: #ff6b81;
  border: none;
  color: white;
  font-size: 20px;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
  transition: 0.3s;
}

.header-button:hover {
  background: #ff4757;
  transform: scale(1.1);
}

/* Cards */
.card-container {
  margin-top: 20px;
}

.card {
  background: #f8f9fa;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
  font-size: 18px;
  color: #fff;
  margin-bottom: 10px;
  transition: transform 0.2s;
}

.card:hover {
  transform: scale(1.02);
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 8px;
}

.card-date {
  font-size: 12px;
  color: rgba(255, 255, 255, 0.8);
}

.delete-btn {
  background: transparent;
  border: none;
  cursor: pointer;
  font-size: 18px;
  color: #fff;
  transition: 0.3s;
}

.delete-btn:hover {
  color: #ff4757;
}

/* Form Overlay */
.form-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
}

.form-box {
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  text-align: center;
  width: 350px;
}

.form-box h2 {
  margin-bottom: 10px;
  font-size: 20px;
  color: #333;
}

.form-close-btn {
  position: absolute;
  top: 10px;
  right: 15px;
  background: none;
  border: none;
  font-size: 25px;
  cursor: pointer;
  color: #555;
}

.form-close-btn:hover {
  color: #ff4757;
}

.form-textarea {
  width: 100%;
  height: 120px;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ddd;
  outline: none;
  font-size: 16px;
  resize: none;
}

.form-save-btn {
  margin-top: 10px;
  padding: 12px 20px;
  background: #28a745;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 16px;
  width: 100%;
  transition: 0.3s;
}

.form-save-btn:hover {
  background: #218838;
}

/* Error Message */
.error-message {
  color: red;
  font-size: 14px;
  margin-bottom: 8px;
}
</style>
