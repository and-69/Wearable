<template>
  <div class="container">
    <div class="clock">
      <div class="home">
        <div class="header">
          <h1>RECOMPENSAS</h1>
          <button @click="$emit('close')">⌂</button>
        </div>
        <div v-if="showModal !== null" class="modal-overlay">
          <div class="modal-content">
            <div v-if="showModal === 0">
              <p>¡Este es tu modal general de recompensa!</p>
            </div>
            <div v-else-if="showModal === 1">
              <p style="text-align: center;">¡BEBIDA ENERGETICA 500ML!</p>
              <div class="contenido">
                <img src="/imgs/pngegg (4).png" alt="" style="width:80px;">
                <div class="precion">⭐300</div>
              </div>
            </div>
            <div v-else-if="showModal === 2">
              <p style="text-align: center;">¡TERMO 1L!</p>
              <div class="contenido">
                <img src="/imgs/pngegg (5).png" alt="" style="width:80px;">
                <div class="precion">⭐1000</div>
              </div>
            </div>
            <div v-else-if="showModal === 3">
              <p style="text-align: center;">¡COLCHONETA DEPORTIVA!</p>
              <div class="contenido">
                <img src="/imgs/pngegg (6).png" alt="" style="width:80px;">
                <div class="precion">⭐1500</div>
              </div>
            </div>
            <div v-else-if="showModal === 4">
              <p style="text-align: center;">¡PAR DE PESAS 1LB!</p>
              <div class="contenido">
                <img src="/imgs/pngegg (7).png" alt="" style="width:80px;">
                <div class="precion">⭐1700</div>
              </div>
            </div>
            <div class="botoncitos">
              <button style="width: 70px; border-radius: 5px;" @click="comprarProducto">🛒</button>
              <button style="width: 70px;" class="btn btn-sm btn-danger" @click="showModal = null">Regresar</button>
            </div>
          </div>
        </div>
        <div class="premios">
          <div class="recompensa" id="recompensa1" @click="openModal(1)">
            <img src="/imgs/pngegg (4).png" alt="">
          </div>
          <div class="recompensa" id="recompensa2" @click="openModal(2)">
            <img src="/imgs/pngegg (5).png" alt="">
          </div>
          <div class="recompensa" id="recompensa3" @click="openModal(3)">
            <img src="/imgs/pngegg (6).png" alt="">
          </div>
          <div class="recompensa" id="recompensa4" @click="openModal(4)">
            <img src="/imgs/pngegg (7).png" alt="">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"
// SweetAlert2 se usa por CDN, disponible como window.Swal
const props = defineProps({ estrellas: Number })
const emit = defineEmits(["comprar", "close"])
const showModal = ref(null)
const precios = [0, 300, 1000, 1500, 1700]

function openModal(num) {
  showModal.value = num
}

function comprarProducto() {
  if (showModal.value) {
    const precio = precios[showModal.value]
    if (props.estrellas >= precio) {
      emit("comprar", precio)
      showModal.value = null
      Swal.fire({
        icon: 'success',
        title: '¡Compra exitosa!',
        text: 'Has canjeado tu recompensa.'
      })
    } else {
      window.Swal.fire({
        icon: 'error',
        title: 'Fondos insuficientes',
        text: 'No tienes suficientes estrellas para esta recompensa.'
      })
    }
  }
}
</script>

<style scoped>
.botoncitos {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin: 20px;
}
.contenido{
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.header {
  color: black;
  display: flex;
  flex-direction: row;
  margin: 0;
  justify-content: space-between;
}
.header button {
  width: 70px;
  border-radius: 45%;
  background-color: rgb(255, 203, 134);
}
.premios {
  margin-top: 30px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
}
.premios img {
  width: 130px;
  height: 130px;
  margin: 20px;
}
img{
    width: 130px;
    height: 130px;
    margin: 20px;
  }
.recompensa {
  background-color: rgb(255, 203, 134);
  margin: 10px;
  border-radius: 20px;
  transition: transform 0.2s, box-shadow 0.2s, background 0.2s;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(26, 132, 144, 0.10);
  display: flex;
  align-items: center;
  justify-content: center;
}
.recompensa:hover {
  transform: scale(1.07) rotate(-2deg);
  background: linear-gradient(120deg, #ffd580 60%, #ffe7b3 100%);
  box-shadow: 0 6px 18px rgba(26, 132, 144, 0.18);
  border: 2px solid #1A8490;
}
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


.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
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
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  max-width: 90%;
  max-height: 80%;
  overflow: auto;
}
@media (max-width:1440px){
  .home{
    width: 380px;
    height: 450px;
  }
  .modal-content, .premios, .contenido, h1, p, .precion, button {
    font-size: 18px;
  }
  .premios img, .contenido img {
    width: 110px;
    height: 110px;
    margin: 14px;
  }
  .header button {
    width: 60px;
    font-size: 18px;
  }
}

@media (max-width:500px){
  .home {
    width: 340px;
    height: 410px;
  }
  .modal-content, .premios, .contenido, h1, p, .precion, button {
    font-size: 16px;
  }
  .premios img, .contenido img {
    width: 90px;
    height: 90px;
    margin: 10px;
  }
  .header button {
    width: 50px;
    font-size: 16px;
  }
}
@media (max-width:450px){
  .home {
    width: 300px;
    height: 370px;
  }
  .modal-content, .premios, .contenido, h1, p, .precion, button {
    font-size: 14px;
  }
  .premios img, .contenido img {
    width: 80px;
    height: 80px;
    margin: 8px;
  }
  .header button {
    width: 45px;
    font-size: 14px;
  }
}
@media (max-width:420px){
  .home {
    width: 270px;
    height: 340px;
    border-radius: 40px;
  }
  .modal-content, .premios, .contenido, h1, p, .precion, button {
    font-size: 13px;
  }
  .premios img, .contenido img {
    width: 60px;
    height: 60px;
    margin: 6px;
  }
  .header button {
    width: 40px;
    font-size: 13px;
  }
}

</style>