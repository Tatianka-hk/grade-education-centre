<template>
  <div class="stars">
    <svg
      v-for="(star, index) in stars"
      :key="index"
      class="star"
      :class="star"
      viewBox="0 0 24 24"
      xmlns="http://www.w3.org/2000/svg"
    >
      <defs>
        <!-- Градієнт для напівзаповненої зірки -->
        <linearGradient id="half-fill" x1="0" x2="1" y1="0" y2="0">
          <stop offset="50%" stop-color="gold" />
          <stop offset="50%" stop-color="lightgray" />
        </linearGradient>
      </defs>

      <!-- Повна зірка -->
      <path
        v-if="star === 'full'"
        fill="gold"
        d="M12 2l3.09 6.26 6.91 1.01-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14l-5-4.87 6.91-1.01L12 2z"
      />

      <!-- Напівзаповнена зірка -->
      <path
        v-else-if="star === 'half'"
        fill="url(#half-fill)"
        d="M12 2l3.09 6.26 6.91 1.01-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14l-5-4.87 6.91-1.01L12 2z"
      />

      <!-- Порожня зірка -->
      <path
        v-else
        fill="lightgray"
        d="M12 2l3.09 6.26 6.91 1.01-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14l-5-4.87 6.91-1.01L12 2z"
      />
    </svg>
  </div>
</template>

<script setup>
import {computed, withDefaults, defineProps} from 'vue'
const props = defineProps({
  rating: Number
})

const stars = computed(() => {
  if (!props) return [];
  const fullStars = Math.floor(props.rating);
  const halfStar = props.rating % 1 >= 0.5 ? 1 : 0; 
  const emptyStars = 5 - fullStars - halfStar; 
  return [
    ...Array(fullStars).fill("full"),
    ...Array(halfStar).fill("half"),
    ...Array(emptyStars).fill("empty"),
  ];
});

</script>
<style>
.stars {
  color: #ffcc00;
  display: flex;
  margin-right: 4px;
  margin-left: 6px;
  align-items: center;
}
.star{
  height: 30px;
  width: 30px;
}
</style>