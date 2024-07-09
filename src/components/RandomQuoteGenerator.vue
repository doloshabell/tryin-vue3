<template>
  <div class="quote-generator">
    <h1 class="app-title">Random Quote Generator</h1>
    <blockquote class="quote-container">
      <p>{{ currentQuote.text }}</p>
      <cite>{{ currentQuote.author }}</cite>
    </blockquote>

    <button @click="getRandomQuote" class="quote-button">Get Random Quote</button>
  </div>
</template>

<script setup>
import {ref, onMounted} from 'vue'

const quotes = ref([
  {
    text: "The only way to great work is to love what you do.",
    author: "Steve Jobs",
  },
  {
    text: "Believe you can do and you're halfway there.",
    author: "Theodore Roosevelt",
  },
  {
    text: "Life is what happens when you're busy making other plans.",
    author: "John Lennon",
  },
]);

let currentIndex = null;

const currentQuote = ref({text: '', author: ''});

const getRandomIndex = () => {
  return Math.floor(Math.random() * quotes.value.length)
}

const getRandomQuote = () => {
  let newIndex;
  do {
    newIndex = getRandomIndex();
  } while (newIndex === currentIndex); // if the getRandomQuotes turns out same as value as before it'll repeat again to call getRandomIndex

  currentIndex = newIndex;
  currentQuote.value = quotes.value[currentIndex];
}

onMounted(getRandomQuote);

</script>

<style scoped>
.quote-generator {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
.app-title {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
}

.quote-container {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #ddd;
  margin-bottom: 20px;
}

p {
  font-size: 18px;
  margin-bottom: 10px;
}

cite {
  font-style: normal;
  color: #777;
}

.quote-button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.quote-button:hover {
  background-color: #2980b9;
}
</style>
