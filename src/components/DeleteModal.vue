<template>
  <Transition name="fade">
    <div v-if="isOpen" class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <h2>{{title}}</h2>
        <p>{{msg}}</p>

        <div class="modal-actions">
          <button class="cancel" @click="closeModal">Скасувати</button>
          <button class="confirm" @click="confirmDeletion">Видалити</button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
defineProps<{ isOpen: boolean,  msg:String; title: String}>();
const emit = defineEmits(["close", "confirm"]);

const closeModal = () => emit("close");
const confirmDeletion = () => emit("confirm");
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  background: white;
  padding: 24px;
  border-radius: 12px;
  width: 90%;
  max-width: 420px;
  text-align: center;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
  animation: scaleIn 0.2s ease-out;
}

.modal-content h2 {
  font-size: 22px;
  margin-bottom: 12px;
  color: #333;
}

.modal-content p {
  font-size: 16px;
  color: #666;
  margin-bottom: 20px;
}

.modal-actions {
  display: flex;
  justify-content: space-between;
  gap: 12px;
}

button {
  flex: 1;
  padding: 10px;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}

.cancel {
  background: #f1f1f1;
  color: #333;
}

.cancel:hover {
  background: #ddd;
}

.confirm {
  background: #e63946;
  color: white;
}

.confirm:hover {
  background: #c72c3b;
}

@keyframes scaleIn {
  from {
    transform: scale(0.9);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>