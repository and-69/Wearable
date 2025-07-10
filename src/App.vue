<template>
  <div class="container">
    <div class="clock">
      <div class="home">
        <h1>{{ stars }}⭐</h1>
        <div>
          <img src="/imgs/globotext.png" alt="" class="texto">
          <div class="colorglobo"></div>
        </div>
        <h2>{{ message }}</h2>
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
          <button type="button" class="btn btn-outline-info">👥</button>
          <button type="button" class="btn btn-outline-light">🎁</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"
const stars = ref("500")
const message = ref("Es momento de trabajar")

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
}

h1 {
  background-color: #f6dcac;
  width: 100px;
  font-size: 30px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: black;
}

.texto {
  height: 150px;
  width: 350px;
}

.colorglobo {
  position: absolute;
  width: 340px;
  height: 108px;
  top: 67px;
  left: 25px;
  background-color: #f6dcac;
  border-radius: 100px;
}

h2 {
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
}

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
.buttons{
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}
.btn{
  width: 60px;
  height: 50px;
  font-size: 25px;
}
.grilla2{
  display: grid;
  grid-template-columns: 1fr 1fr;
}
</style>