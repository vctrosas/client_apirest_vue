<script setup>
import axios from 'axios'
import { ref } from 'vue'




const empleados = ref([])

const getData = async () => {
    try {
      const { data } = await axios.get('http://laravelapi.test/api/empleado', {
         headers: {
            Authorization: "Bearer 2|88g2ESQVUmVMdFMB6kvcbt4UjPXdOjl6rFpdx99l"
          }
      })
      empleados.value = data;
      
    } catch (error) {
      console.log(error)
    }
} 
getData();

const editar = (id) => {
 
  window.location.href='/editar/'+id;
}

</script>

<template>
       <h1>Tabla Empleados</h1>
      <table>
        <thead>
          <tr>
            <th >#</th>
            <th >First Name</th>
            <th >Last Name</th>
            <th >Full Name</th>
            <th >Job Title</th>
            <th >Age</th>
            <th >Birthday</th>
            <th >Editar</th>
         
          </tr>
        </thead>
        <tbody>
        <tr v-for="emp in empleados" :key="emp.id">
          <th>{{emp.id}}</th>
          <td>{{emp.first_name}}</td>
          <td>{{emp.last_name}}</td>
          <td>{{emp.full_name}}</td>
          <td>{{emp.job_position}}</td>
          <td>{{emp.age}}</td>
          <td>{{emp.birthday}}</td>
         
          <td><button @click="editar(emp.id)" >Editar</button></td>
          
        
        </tr>
      
      </tbody>
      </table>
</template>
<style scoped>
body{
    background-color:white; 
}
table{
  width:100%;
}
table thead th{
    color:black;
    background-color:white;
}
table thead{
    border:1px solid white;
}
table tbody tr{
    color:silver;
    
}
table tbody td{
  border-bottom:2px solid gray;
}
.item {
  margin-top: 2rem;
  display: flex;
}

.details {
  flex: 1;
  margin-left: 1rem;
}

i {
  display: flex;
  place-items: center;
  place-content: center;
  width: 32px;
  height: 32px;

  color: var(--color-text);
}

h3 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--color-heading);
}

@media (min-width: 1024px) {
  .item {
    margin-top: 0;
    padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
  }

  i {
    top: calc(50% - 25px);
    left: -26px;
    position: absolute;
    border: 1px solid var(--color-border);
    background: var(--color-background);
    border-radius: 8px;
    width: 50px;
    height: 50px;
  }

  .item:before {
    content: ' ';
    border-left: 1px solid var(--color-border);
    position: absolute;
    left: 0;
    bottom: calc(50% + 25px);
    height: calc(50% - 25px);
  }

  .item:after {
    content: ' ';
    border-left: 1px solid var(--color-border);
    position: absolute;
    left: 0;
    top: calc(50% + 25px);
    height: calc(50% - 25px);
  }

  .item:first-of-type:before {
    display: none;
  }

  .item:last-of-type:after {
    display: none;
  }
}
</style>