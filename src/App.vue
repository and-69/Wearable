<template>
  <div>
    <formulario v-if="showForm" @form-submitted="handleFormSubmit" />
    <recompensas v-else-if="showRecompensas" @close="cerrarRecompensas" />
    <personas v-else-if="showPersonas" @close="cerrarPersonas" />
    <div v-else>
      <div class="container">
        <div class="clock">
          <div class="home">
            <h1>{{ stars }}⭐</h1>
            <div class="comic-bubble">
              <h2>{{ message }}</h2>
            </div>

            <div class="grilla">
              <div>
                <img src="/imgs/base.gif" alt="" class="gifprincipal">
              </div>
              <div class="datos">
                <div class="encabezadotarjet">
                  <img src="/imgs/corazon.png" alt="" class="corazon">
                  <img src="/imgs/ritmo.png" alt="" class="ritmo">
                </div>
                <hr>
                <hr>
                <div class="grilla2">
                  <h3></h3>
                  <div>
                  </div>
                  <div>
                  </div>
                </div>
              </div>
            </div>
            <div class="buttons">
              <button type="button" class="btn btn-outline-info" @click="abrirPersonas">👥</button>
              <button type="button" class="btn btn-outline-light" @click="abrirRecompensas">🎁</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"
import formulario from "./components/formulario.vue"
import recompensas from "./components/recompensas.vue"
import personas from "./components/personas.vue"

const stars = ref("500")
const message = ref("Es momento de trabajar")
const showForm = ref(true)
const userData = ref([])
const showRecompensas = ref(false)
const showPersonas = ref(false)

function handleFormSubmit(data) {
  userData.value = [data]
  showForm.value = false
}
function abrirRecompensas() {
  showRecompensas.value = true
}
function cerrarRecompensas() {
  showRecompensas.value = false
}
function abrirPersonas() {
  showPersonas.value = true
}
function cerrarPersonas() {
  showPersonas.value = false
}
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

h1 {
  background-color: #f6dcac;
  width: 100px;
  font-size: 30px;
  border-radius: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: black;
}

.comic-bubble {
  background-image: url('/imgs/globotext.png');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  width: 400px;
  height: 280px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 20px;
  font-family: 'Comic Sans MS', cursive;
  font-size: 18px;
  color: #000;
}


/* h2 {
  width: 300px;
  word-wrap: break-word;
  overflow-wrap: break-word;
  padding: 0 20px;
  margin: 0;
  font-size: 18px;
  line-height: 1.4;
  position: relative;
  top: -130px;
  color: black;
} */

.gifprincipal {
  width: 200px;
  position: relative;
  top: -50px;
  left: -40px;
}

.grilla {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.datos {
  border: 1px solid #01204E;
  position: relative;
  top: -50px;
  left: -20px;
  padding: 10px;
}

.ritmo,
.corazon {
  width: 50px;
  height: 50px;
}

.encabezadotarjet {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

hr {
  height: 1px;
  margin: 5px;
  color: #01204E;
}

.buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

.btn {
  width: 60px;
  height: 50px;
  font-size: 25px;
  border-radius: 50%;
}

.grilla2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
</style>