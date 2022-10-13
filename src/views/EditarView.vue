<script setup>
import axios from 'axios'
import { ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

const empleados = ref([])


const getData = async () => {
    try {
      const { data } = await axios.get(`http://laravelapi.test/api/empleado/${route.params.id}`, {
         headers: {
            Authorization: "Bearer 2|88g2ESQVUmVMdFMB6kvcbt4UjPXdOjl6rFpdx99l"
          }
      })
      
        empleados.value = data;
        //const firstNames = empleados.value.map(name => name.first_name)
        //console.log(firstName);
      
    } catch (error) {
      console.log(error)
    }
} 
getData();



const editar = (iden) => {
    axios.defaults.headers.common["Authorization"] = "Bearer 2|88g2ESQVUmVMdFMB6kvcbt4UjPXdOjl6rFpdx99l";
    //alert(firstName.value);
    
    const update = async () => {
        try {
            const { data } = await axios.put(`http://laravelapi.test/api/empleado/update`, {
                
                id: iden,
                first_name: firstName.value,
                last_name: lastName.value,
                full_name: firstName.value + ' ' +lastName.value,
                job_position: jobPosition.value,
                birthday: birthday.value,
            
            })
            alert('Se han actualizado con exito los datos');
        } catch (error) {
            alert("Debes completar toda la información");
        }

    }
    update();
}
</script>

<template>
<h1>Editar</h1>
<div class="mb-3" v-for="emp in empleados" :key="emp.id">
  <label for="firstName"  class="form-label">First Name</label>
  <input type="input" class="form-control" id="firstName" :value="`${emp.first_name}`" >
  <label for="lastName" class="form-label">Last Name</label>
  <input type="input" class="form-control" id="lastName" :value="`${emp.last_name}`">
  <label for="jobPosition" class="form-label">Job Position</label>
  <input type="input" class="form-control" id="jobPosition" :value="`${emp.job_position}`">
  <label for="birthday" class="form-label">Birthday</label>
  <input type="input" class="form-control" id="birthday" :value="`${emp.birthday}`">
  <br>
  <button type="button" class="btn btn-danger" @click="editar(emp.id)">Guardar</button>
</div>
</template>