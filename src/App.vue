<script setup lang="ts">
import { ref, onMounted } from "vue";
import axios from 'axios';
import Button1 from './components/Button.vue'
import DeleteModal from "./components/DeleteModal.vue";
import {ReviewData} from './types'
// import 'dotenv/config'
const showModal = ref(false);
const apiUrl = import.meta.env.VITE_API_URL; 
console.log(apiUrl)
const reviewData = ref<ReviewData | null>(null);

const deleteMessage = () => {
  console.log("Повідомлення видалено!");
  showModal.value = false;
};

onMounted(async () => {
  try {
    const response = await axios.get(apiUrl);
    reviewData.value = response.data[0];
  } catch (error) {
    console.error('Помилка отримання даних:', error);
  }
});

</script>

<template>
  <Button1  title="Відгуки наших клієнтів у Google" :reviewData="reviewData"/>
  <button @click="showModal = true" class="delete-button">Видалити повідомлення</button>
  <DeleteModal :isOpen="showModal" @close="showModal = false" @confirm="deleteMessage" title="Видалення повідомлення" msg="Ви точне хочите видалити дане повідомлення?"/>
</template>

<style scoped>
.delete-button{
  margin-top: 45px;
}
</style>
