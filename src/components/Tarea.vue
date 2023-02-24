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
            <ul class="list-group">
              <li v-for="(tarea, index) of listTareas" :key="index"
              class="list-group-item d-flex justify-content-between">
                <span class="cursor">
                  <i class="fa-sharp fa-regular fa-circle"></i>
                </span>
                {{ tarea.nombre }}
                <span class="text-danger cursor">
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
      }
    }
  }
</script>

<style scoped>
  .cursor {
    cursor: pointer;
  }
</style>