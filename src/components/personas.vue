<template>
  <div class="container">
    <div class="clock">
      <div class="home">
        <div class="tabs">
          <button :class="{active: tab==='grupal'}" @click="tab='grupal'">Grupal</button>
          <button :class="{active: tab==='perfil'}" @click="tab='perfil'">Perfil</button>
        </div>
        <div class="tab-content">
          <div v-if="tab==='grupal'" class="grupo-scroll">
            <h2>Grupo</h2>
            <ul>
              <li v-for="persona in personasGrupales" :key="persona.id" >
                {{ persona.name }} {{ persona.surname }} - {{ persona.ocupation }} | <b>Monedas:</b> {{ persona.monedas }}⭐
              </li>
            </ul>
            <div style="margin-top:10px;font-weight:bold;">
              Total monedas del grupo: {{ totalMonedas }} ⭐
            </div>
          </div>
          <div v-else>
            <h2>Perfil</h2>
            <div v-if="perfil" class="perfil-scroll" >
              <p><b>ID:</b> {{ perfil.id }}</p>
              <p><b>Nombre:</b> {{ perfil.name }} {{ perfil.surname }}</p>
              <p><b>Fecha de nacimiento:</b> {{ perfil.birthdate }}</p>
              <p><b>Género:</b> {{ perfil.gender }}</p>
              <p><b>Estado civil:</b> {{ perfil.marital }}</p>
              <p><b>Ocupación:</b> {{ perfil.ocupation }}</p>
              <p><b>Nivel de estudios:</b> {{ perfil.scolary }}</p>
              <p><b>Hábitos:</b></p>
              <ul>
                <li>Fumar: {{ perfil.habitos?.fumar }}</li>
                <li>Alcohol: {{ perfil.habitos?.alcohol }}</li>
                <li>Ejercicio: {{ perfil.habitos?.ejercicio }}</li>
              </ul>
              <p><b>Condiciones médicas:</b> {{ perfil.condicionesSeleccionadas?.join(', ') }}</p>
            </div>
            <div v-else>
              <p>No hay datos de perfil disponibles.</p>
            </div>
          </div>
        </div>
        <button class="btn btn-primary mt-3" @click="volverHome">Home</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"
defineProps({perfil: Object})
const tab = ref('grupal')
function randomMonedas() {
  return Math.floor(Math.random() * 500 + 50)
}
const personasGrupales = ref([
  {id: 1, name: 'Ana', surname: 'García', ocupation: 'Ingeniera', monedas: randomMonedas()},
  {id: 2, name: 'Luis', surname: 'Martínez', ocupation: 'Doctor', monedas: randomMonedas()},
  {id: 3, name: 'Sofía', surname: 'López', ocupation: 'Estudiante', monedas: randomMonedas()},
  {id: 4, name: 'Carlos', surname: 'Ruiz', ocupation: 'Profesor', monedas: randomMonedas()},
  {id: 5, name: 'Marta', surname: 'Torres', ocupation: 'Niñera', monedas: randomMonedas()},
  {id: 6, name: 'Pedro', surname: 'Nieves', ocupation: 'Abogado', monedas: randomMonedas()},
  {id: 7, name: 'Lucía', surname: 'Castro', ocupation: 'Psicóloga', monedas: randomMonedas()},
  {id: 8, name: 'Jorge', surname: 'Pérez', ocupation: 'Contador', monedas: randomMonedas()},

])
const totalMonedas = ref(personasGrupales.value.reduce((acc, p) => acc + p.monedas, 0))


try {
  perfil = JSON.parse(localStorage.getItem('perfil'))
} catch(e) {}

const emit = defineEmits(['close'])
function volverHome() {
  emit('close')
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
.tabs {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 15px;
}
.tabs button {
  padding: 8px 18px;
  border-radius: 20px;
  border: none;
  background: #f6dcac;
  color: #1A8490;
  font-weight: bold;
  cursor: pointer;
}
.tabs button.active {
  background: #1A8490;
  color: #fff;
  border: 2px solid #f6dcac;
}
.tab-content {
  background: #fff2;
  border-radius: 16px;
  padding: 12px;
  min-height: 200px;
  margin-bottom: 10px;
}
.btn-primary {
  background: #028391;
  color: #fff;
  border: none;
  border-radius: 20px;
  padding: 8px 24px;
  font-size: 18px;
  cursor: pointer;
}
.perfil-scroll {
  height: 250px;
  overflow-y: auto;
}
.grupo-scroll {
  height: 250px;
  overflow-y: auto;
}
@media(max-width:1440px){
  .home {
    width: 380px;
    height: 450px;
  }
  .tabs button {
    padding: 6px 14px;
    font-size: 14px;
  }
  .btn-primary {
    padding: 6px 20px;
    font-size: 16px;
  }

}
@media (max-width:500px){
  .home {
    width: 350px;
    height: 430px;
  }
  .tab-content, .perfil-scroll, .grupo-scroll, h2, p, ul, li {
    font-size: 16px;
  }
  .tabs button {
    font-size: 14px;
  }
  .btn-primary {
    font-size: 15px;
  }
}
@media (max-width:470px){
  .home {
    width: 320px;
    height: 400px;
  }
  .tab-content, .perfil-scroll, .grupo-scroll, h2, p, ul, li {
    font-size: 15px;
  }
  .tabs button {
    font-size: 13px;
  }
  .btn-primary {
    font-size: 14px;
  }
}
@media (max-width:440px){
  .home {
    width: 300px;
    height: 380px;
  }
  .tab-content, .perfil-scroll, .grupo-scroll, h2, p, ul, li {
    font-size: 14px;
  }
  .tabs button {
    font-size: 12px;
  }
  .btn-primary {
    font-size: 13px;
  }
}
@media (max-width:420px){
  .home {
    width: 280px;
    height: 360px;
    border-radius: 40px;
  }
  .tab-content, .perfil-scroll, .grupo-scroll, h2, p, ul, li {
    font-size: 13px;
  }
  .tabs button {
    font-size: 11px;
  }
  .btn-primary {
    font-size: 12px;
  }
}
@media (max-width:400px){
  .home {
    width: 260px;
    height: 340px;
  }
  .tab-content, .perfil-scroll, .grupo-scroll, h2, p, ul, li {
    font-size: 12px;
  }
  .tabs button {
    font-size: 10px;
  }
  .btn-primary {
    font-size: 11px;
  }
}
</style>