<template>
  <div class="container">
    <div class="clock">
      <div class="home">
        <button type="button" class="btn btn-outline-light" @click="showModal = true">🎁</button>
        <div v-if="showModal" class="modal-overlay">
          <div class="modal-content">
            <p>¡Este es tu modal de recompensa!</p>
            <button class="btn btn-sm btn-danger" @click="showModal = false">Cerrar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"
const showModal = ref(false)
</script>

<style scoped>
.home {
  position: absolute;
  width: 415px;
  height: 510px;
  top: 50%;
  left: 50.1%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  border-radius: 60px;
  background-color: #1A8490;
  padding: 20px;
  overflow: hidden;
}

/* Modal styles */
.modal-overlay {
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.modal-content {
  background: #fff;
  color: #222;
  padding: 20px 30px;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
  max-width: 90%;
  max-height: 80%;
  overflow: auto;
}
</style>