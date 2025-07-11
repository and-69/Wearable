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
                    <input type="text" class="form-control" placeholder="Enter your occupation" v-model="form.ocupation">
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
            <div class="row">
              <button type="button" class="btn btn-warning" @click="goToForm2">Enter</button>
            </div>
            
        </div>
    </div>
</template>


<script setup>
import { ref } from "vue"
const emit = defineEmits(['form-submitted'])
const form = ref({
  id: "",
  name: "",
  surname: "",
  birthdate: "",
  gender: "",
  marital: "",
  ocupation: "",
  scolary: ""
})

function goToForm2() {
  emit('form-submitted', { ...form.value }) 
}
</script>


<style scoped>
.formulario{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px 50px;
    margin: 0 150px;
    background-color: #028391;
    position: relative;
    top: 150px;
    border-radius: 20px;
    gap: 10px;
}
.row{
    display: flex;
    gap: 10px;
}
p{
  margin-bottom: 0;
}
</style>