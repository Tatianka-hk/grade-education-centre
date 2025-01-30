<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import axios from 'axios';
import Stars from './Stars.vue'

interface ReviewData {
  rating: number;
  reviews: number;
}

const reviewData = ref<ReviewData | null>(null);
const apiUrl = 'https://679b54ed33d31684632379e8.mockapi.io/api/button1/b1'; 
onMounted(async () => {
  try {
    const response = await axios.get(apiUrl);
    reviewData.value = response.data[0];
  } catch (error) {
    console.error('Помилка отримання даних:', error);
  }
});


const redirectToGoogle = () => {
  window.location.href = 'https://www.google.com';
};

const showMessage = () => {
  alert('Дякуємо за відгук!');
};
</script>

<template>
    <div class="review-card">
      <div class="review-head">
        <div class="review-header">
          <img src="https://cdn-icons-png.flaticon.com/512/2991/2991148.png" alt="Google Logo" class="google-logo" />
          <span class="review-header-text">Відгуки наших клієнтів у Google</span>
        </div>
        <div class="review-content" v-if="reviewData">
          <span class="review-content-rating">
            <span class="rating">{{ reviewData.rating }}</span>
          <Stars :rating="reviewData.rating"/>
          </span>
          <span class="reviews">{{ reviewData.reviewsCount }} відгуки</span>
        </div>
      </div>
      <div class="review-buttons">
        <button @click="redirectToGoogle" class="btn btn-secondary">Переглянути</button>
        <button @click="showMessage" class="btn btn-primary">Написати</button>
      </div>
    </div>
</template>

<style scoped>

.review-card {
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
  text-align: center;
  max-width: 1458px;
  width: 1458px;
  display: flex;
  justify-content: space-between;
  padding: 30px;
  align-items: center;
}

.review-head{
  display: flex;
  gap:60px;
}

.review-header {
  display: flex;
  align-items: center;
  gap: 20px;
  font-size: 16px;
  font-weight: 500;
}
.review-header-text{
  font-family: Formular;
  font-weight: 600;
  font-size: 20px;
  line-height: 30px;
  color: rgba(57, 65, 85, 1);
}
.google-logo {
  width: 40px;
  height: 40px;
}

.review-content {
  display: flex;
  gap:20px;
  height: 44px;
  align-items: center;
}
.review-content-rating{
  display: flex;
  height: 44px;
  align-items: center;
}
.rating{
  font-family: Creenwich ;
  font-weight: 600;
  font-size: 24px;
  line-height: 34px;
  color: rgba(57, 65, 85, 1);
}

.reviews{
  font-family: Formular;
  font-weight: 400;
  font-size: 14px;
  line-height:22px;
  color:rgba(121, 133, 149, 1);
}


.review-buttons {
  display: flex;
  gap: 10px;
  justify-content: center;
}

.btn {
  padding: 10px 20px;
  border-radius: 8px;
  font-size: 14px;
  cursor: pointer;
  height: 44px;
}

.btn-primary {
  background: linear-gradient(to right, rgba(60, 185, 160, 1), rgba(23, 134, 172, 1));
  color: white;
  width: 109px;
  border: none;
}

.btn-secondary {
  color: black;
  border: 1px solid linear-gradient(to right, rgba(170, 206, 219, 1), rgba(190, 226, 224, 1));
  background: linear-gradient(to right, rgba(230, 247, 245, 1), rgba(248, 252, 252, 1));
  width: 132px;
}






@media (max-width: 1367px ) {
  .review-card {
    max-width: 1286px;
    width: 1286px;

  }
  
  .review-head{
    gap:50px;
  }
  
}

@media (max-width: 1199px ) {
  .review-card {
    max-width: 912px;
    width: 100%;
  }
  .review-head{
    display: grid;
    gap:10px;
  }
  
}


@media (max-width: 576px) {
  .review-card {
    max-width: 328px;
    width: 328px;
  }

  .review-card{
    display: grid;
  }

  .review-buttons {
    flex-direction: column;
  }

  .review-head{
    display: grid;
    gap:20px;
    width: 268px;
  }

  .review-content{
    display: grid;
    height: 60px;
    gap: 0px;
    margin-bottom: 20px;
  }
  .reviews{
    text-align: start;
  }
  .btn{
    width: 268px;
  }
}
</style>
