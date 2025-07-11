<template>
    <div class="container">
        <div class="formulario">
            <h1>Registration Form</h1>
            <div class="row">
                <div class="col-md-12">
                    <input type="number" class="form-control" placeholder="Enter your ID" v-model="form.id">
                </div>
                <div class="col-md-12">
                    <input type="text" class="form-control" placeholder="Enter your first name" v-model="form.name">
                </div>
                <div class="col-md-12">
                    <input type="text" class="form-control" placeholder="Enter your last name" v-model="form.surname">
                </div>
                <div class="col-md-12">
                    <p>Birthday</p>
                    <input type="date" class="form-control" v-model="form.birthdate">
                </div>
                <div class="col-md-12">
                    <select class="form-select" aria-label="Default select example" v-model="form.gender">
                        <option selected disabled value="">Select your gender</option>
                        <option value="Female">Female</option>
                        <option value="Male">Male</option>
                        <option value="Other">Other</option>
                    </select>
                </div>
                <div class="col-md-12">
                    <select class="form-select" aria-label="Default select example" v-model="form.marital">
                        <option selected disabled value="">Select your marital status</option>
                        <option value="Married">Married</option>
                        <option value="Single">Single</option>
                        <option value="Divorced">Divorced</option>
                        <option value="Widowed">Widowed</option>
                    </select>
                </div>
                <div class="col-md-12">
                    <input type="text" class="form-control" placeholder="Enter your occupation"
                        v-model="form.ocupation">
                </div>
                <div class="col-md-12">
                    <select class="form-select" aria-label="Default select example" v-model="form.scolary">
                        <option selected disabled value="">Select your study level</option>
                        <option value="HighSchool">High School</option>
                        <option value="Vocational">Vocational Training (VT)</option>
                        <option value="University">University Studies</option>
                        <option value="Special">Special Regime Studies</option>
                    </select>
                </div>
            </div>
            <br>
            <!-- Hábitos Personales -->
            <div class="row">
                <h5 class="mb-3">Hábitos personales</h5>
                <div class="col-md-12">
                    <label class="form-label">¿Fumas regularmente?</label>
                    <select class="form-select" v-model="form.habitos.fumar">
                        <option value="" disabled>Selecciona una opción</option>
                        <option>Sí</option>
                        <option>No</option>
                        <option>Ocasionalmente</option>
                    </select>
                </div>
                <div class="col-md-12">
                    <label class="form-label">¿Consumes bebidas alcohólicas?</label>
                    <select class="form-select" v-model="form.habitos.alcohol">
                        <option value="" disabled>Selecciona una opción</option>
                        <option>Sí</option>
                        <option>No</option>
                        <option>Socialmente</option>
                    </select>
                </div>
                <div class="col-md-12">
                    <label class="form-label">¿Realizas actividad física regularmente?</label>
                    <select class="form-select" v-model="form.habitos.ejercicio">
                        <option value="" disabled>Selecciona una opción</option>
                        <option>Más de 3 veces por semana</option>
                        <option>1–2 veces por semana</option>
                        <option>No</option>
                    </select>
                </div>
            </div>

            <!-- Condiciones médicas -->
            <div class="row centrar">
                <h5 class="mb-3">Condiciones médicas</h5>
                <div class="col-md-12">
                    <label class="form-label">¿Tienes alguna de estas condiciones?</label>
                    <div class="form-check" v-for="condicion in listaCondiciones" :key="condicion">
                        <input class="form-check-input" type="checkbox" :id="condicion" :value="condicion"
                            v-model="form.condicionesSeleccionadas" />
                        <label class="form-check-label" :for="condicion">
                            {{ condicion }}
                        </label>
                    </div>
                </div>
            </div>

            <div class="row">
                <button type="button" class="btn btn-warning" @click="goToForm2">Enter</button>
            </div>

        </div>
    </div>
</template>


<script setup>
import { ref } from "vue"
const emit = defineEmits(['form-submitted'])
const listaCondiciones = [
    "Diabetes",
    "Hipertensión",
    "Cardiopatía",
    "Obesidad",
    "Asma",
    "Otra"
]
const form = ref({
    id: "",
    name: "",
    surname: "",
    birthdate: "",
    gender: "",
    marital: "",
    ocupation: "",
    scolary: "",
    habitos: {
        fumar: "",
        alcohol: "",
        ejercicio: ""
    },
    condicionesSeleccionadas: []
})
const usuarios = ref([])
const errorMsg = ref("")
function goToForm2() {
    if (
        !form.value.id ||
        !form.value.name ||
        !form.value.surname ||
        !form.value.birthdate ||
        !form.value.gender ||
        !form.value.marital ||
        !form.value.ocupation ||
        !form.value.scolary
    ) {
        Swal.fire({
            icon: 'error',
            title: 'Campos obligatorios',
            text: 'Por favor, completa todos los campos, son obligatorios.'
        })
        return
    }
    usuarios.value.push({ ...form.value })
    Swal.fire({
        icon: 'success',
        title: '¡Registro exitoso!',
        text: 'Tus datos han sido guardados correctamente.'
    })
    emit('form-submitted', { ...form.value })
}
</script>


<style scoped>
.formulario {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px 50px;
    margin: 0 150px;
    background-color: #028391;
    position: relative;
    top: 20px;
    border-radius: 20px;
    gap: 10px;
}

.row {
    display: flex;
    gap: 10px;
}

p {
    margin-bottom: 0;
}

.centrar {
    display: flex;
    flex-direction: column;
    align-items: center;
}

@media (max-width: 768px) {
    .formulario {
        width: 100%;
        margin: 0;
        padding: 20px;
    }
}
</style>