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
              <div v-if="etapa === 'trabajo' || etapa === 'pausa'" class="timer">
                <span>⏰ {{ Math.floor(timeLeft / 60).toString().padStart(2, '0') }}:{{ (timeLeft %
                  60).toString().padStart(2, '0') }}</span>
              </div>
            </div>

            <div class="grilla">
              <div>
                <img :src="gifSrc" :class="['gifprincipal', etapa === 'pausa' ? 'gif-pausa' : '']" alt="" />
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
import { ref, onMounted, onUnmounted } from "vue"
import formulario from "./components/formulario.vue"
import recompensas from "./components/recompensas.vue"
import personas from "./components/personas.vue"

const stars = ref(500)
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

const etapa = ref("trabajo")
const timeLeft = ref(60)
const gifSrc = ref("/imgs/base.gif")
let timer = null

function startTrabajo() {
  etapa.value = "trabajo"
  timeLeft.value = 60
  message.value = "¡Es momento de trabajar!"
  gifSrc.value = "/imgs/base.gif"
  if (timer) clearInterval(timer)
  timer = setInterval(() => {
    if (timeLeft.value > 0) {
      timeLeft.value--
    } else {
      clearInterval(timer)
      startPausa()
    }
  }, 1000)
}

function startPausa() {
  etapa.value = "pausa"
  timeLeft.value = 60
  message.value = "¡Hora de una pausa activa!"
  gifSrc.value = "/imgs/pausas.gif"
  if (timer) clearInterval(timer)
  timer = setInterval(() => {
    if (timeLeft.value > 0) {
      timeLeft.value--
    } else {
      clearInterval(timer)
      startRecompensa()
    }
  }, 1000)
}

function startRecompensa() {
  etapa.value = "recompensa"
  const recompensa = 50
  message.value = `¡Ganaste ${recompensa} monedas!`
  gifSrc.value = "/imgs/recompensa.gif"
  stars.value += recompensa
  setTimeout(() => {
    startTrabajo()
  }, 3000)
}

onMounted(() => {
  startTrabajo()
})

onUnmounted(() => {
  if (timer) clearInterval(timer)
})
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
  box-sizing: border-box;
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
  background-size: 100% 100%;
  background-repeat: no-repeat;
  background-position: center;
  text-align: center;
  width: 300px;
  height: 120px; 
  font-family: 'Comic Sans MS', cursive;
  font-size: 18px;
  color: #000;
  margin: 0 auto 10px auto;
  box-sizing: border-box;
  padding: 24px 16px;
}


h2 {
  width: 300px;
  padding: 0 20px;
  margin: 0;
  font-size: 18px;
  color: black;
}

.gifprincipal {
  width: 200px;
  position: relative;
}

.grilla {
  display: grid;
  grid-template-columns: 1fr 1fr;
  overflow: hidden;
}

.datos {
  border: 1px solid #01204E;
  position: relative;
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
  margin-top: 20px;
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
.gif-pausa {
  width: 160px;
  height: 220px;
}
@media (max-width:1440px){
  .home{
    width: 380px;
    height: 450px;
  }
  .gifprincipal {
    width: 150px;
  }
  .gif-pausa {
    width: 130px;
    height: 150px;
  }
}
@media (max-width:500px){
  .home {
    width: 350px;
    height: 430px;
  }
  .gifprincipal {
    width: 140px;
  }
  .gif-pausa {
    width: 100px;
    height: 150px;
  }
  h1 {
    width: 80px;
    font-size: 20px;
  }
  @media (max-width:470px){
    .home {
      width: 320px;
      height: 400px;
    }
    .gifprincipal {
      width: 120px;
    }
    .gif-pausa {
      width: 100px;
      height: 120px;
    }
    h1 {
      width: 70px;
      font-size: 18px;
    }
  }
  @media (max-width:440px){
    .home {
      width: 300px;
      height: 380px;
    }
    .comic-bubble{
      width: 250px;

    }
    h2{
      width: 240px;
      font-size: 16px;
    }
    .gifprincipal {
      width: 100px;
    }
    .gif-pausa {
      width: 80px;
      height: 100px;
    }
    h1 {
      width: 60px;
      font-size: 16px;
    }
  }
  @media (max-width:420px){
    .home {
      width: 280px;
      height: 360px;
    }
    .comic-bubble{
      width: 220px;
      height: 100px;
      padding: 10px 10px;
    }
    h2{
      width: 200px;
      font-size: 14px;
    }
    .datos{
      padding: 5px;
    }
    .gifprincipal {
      width: 80px;
    }
    .gif-pausa {
      width: 70px;
      height: 90px;
    }
    h1 {
      width: 50px;
      font-size: 14px;
    }
  }
  @media (max-width:400px){
    .home {
      width: 270px;
      height: 330px;
    }
    span{
      font-size: 15px;
    }
    .comic-bubble{
      width: 200px;
      height: 90px;
      padding: 8px 8px;
    }
    h2{
      width: 180px;
      font-size: 15px;
    }
    .datos{
      padding: 3px;
    }
    .gifprincipal {
      width: 70px;
    }
    .gif-pausa {
      width: 60px;
      height: 80px;
    }
    h1 {
      width: 40px;
      font-size: 12px;
    }
  }
}
</style>
