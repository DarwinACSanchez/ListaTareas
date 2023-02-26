<template>
  <div>
    <h1 class="display-4 text-center">Listado de Tareas</h1>
    <hr>
    <div class="row">
      <div class="col-lg-8 offset-lg-2">
        <div class="card mt-4">
          <div class="card-body">
            <div class="input-group">
              <input type="text" v-model="tarea" 
              class="form-control form-control-lg" placeholder="Agregar Tarea">
              <div class="input-group-append">
                <button v-on:click="agregarTarea()"
                class="btn btn-success btn-lg">Agregar</button>
              </div>
            </div>
            <br>
            <h5 v-if="listTareas == 0">No hay Tareas para Realizar</h5>
            <ul class="list-group">
              <!-- ciclo for para recorre el array -->
              <li v-for="(tarea, index) of listTareas" :key="index"
              class="list-group-item d-flex justify-content-between">
              <!-- si es verdadero pone el cleck en verde -->
                <span class="cursor" v-bind:class="{'text-success': tarea.estado}" 
                v-on:click="editarTarea(tarea, index)">
                  <!-- cambia el icono si esta clicleado o no  -->
                  <i v-bind:class="[tarea.estado ? 'fa-solid fa-circle-check' : 'fa-sharp fa-regular fa-circle']"></i>
                </span>
                {{ tarea.nombre }}
                <span class="text-danger cursor" v-on:click="eliminarTarea(tarea.id)">
                  <i class="fa-solid fa-trash-can"></i>
                </span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

  export default {
    name: 'Tarea',
    data() {
      return {
        tarea: '',
        listTareas: []
      }
    },
    methods: {
      agregarTarea() {
        const tarea = {
          nombre: this.tarea, //accedemos a esa variable
          estado: false
        }
        this.listTareas.push(tarea); //agregamos al array
        this.tarea = ''; //limpia el combo
      },
      eliminarTarea(id) {
        //this.listTareas.splice(index, 1) //elimina un elemento
        axios.delete("https://localhost:44323/api/Tarea/" + id).then(response => {
          console.log(response);
        }).catch(error => {
          console.log(error)
        });
      },
      editarTarea(tarea, index) {
        this.listTareas[index].estado = !tarea.estado
      },
      obtenerTareas() {
        axios.get("https://localhost:44323/api/Tarea").then(response => {
          console.log(response);
          this.listTareas = response.data;
        })
      }
    },
    created: function() {
      this.obtenerTareas();
    }
  }
</script>

<style scoped>
  .cursor {
    cursor: pointer;
  }
</style>