<template>
  <div id="app">
     <div id="col" class="columns is-desktop">
         <div class="column">
             <h1>Gestor de Tareas</h1>
             <h5>Agrega la cantidad de tareas que usted necesite
                 en cualquier momento puede quitarlas</h5>
         </div>
     </div>
      <div id="input" class="columns is-desktop">
          <div class="column is-half is-offset-one-quarter">
             <p>Coloque el nombre de la tarea</p>
              <input v-model="tareas.nombre" class="input is-primary" type="text" placeholder="nombre">
              <p>Coloque la cantidad de horas que le llevara</p>
              <input v-model="tareas.hora" class="input is-primary" type="number" placeholder="0">
              <textarea v-model="tareas.descripcion" class="textarea" placeholder="Descripcion de la tarea"></textarea>
            <div class="field is-grouped is-grouped-right">
              <p class="control">
                <a @click="guardar" class="button is-primary">Agregar</a>
              </p>
              <p class="control">
                <a @click="noGuardar" class="button is-light">Cancel</a>
              </p>
            </div>
          </div>
      </div>
      <div id="title" class="columns">
          <div class="column">
              <h1>Tus tareas asignadas</h1>
              <div class="divider"></div>
          </div>
      </div>
      <div id="tareas" class="columns">
          <div class="column is-8 is-offset-2">
              <article v-for="t in tareas" class="message is-info">
                  <div class="message-header">
                        <p>{{ t.nombre }}</p>
                     <button @click="borrar" class="delete"></button>
                  </div>
                  <div class="message-body">
                        <p>Cantidad de horas que te llevara: {{ t.hora | masUno}}</p>
                        <p class="divider"></p>
                        <p>{{ t.descripcion }}</p>
                  </div>
            </article>
          </div>
      </div>
     <br>
     <box></box>
  </div>
</template>

<script>
import box from './components/box'    
export default {
  name: 'app',
  data () {
    return {
      tareas: [
          { nombre: '', hora:'', descripcion: ''}
        ] 
    }
 },
  components: {
      box
  },
  methods: {
      guardar () {
//incluye un nuevo array a la lista          
          this.tareas.push({
              nombre: this.tareas.nombre,//nombre de la tarea
              hora: this.tareas.hora,
              descripcion: this.tareas.descripcion
        })
//esta linea agrega a localstorage la tarea            
          localStorage.setItem("tareas", JSON.stringify(this.tareas))
          this.tareas.nombre = ''
          this.tareas.hora = ''
          this.tareas.descripcion = ''
      },
      noGuardar () {
//settea todas las variables a valor null          
          this.tareas.nombre = ''
          this.tareas.hora = ''
          this.tareas.descripcion = ''
      },
      borrar (index) {
          this.tareas.splice(index, 1)
      localStorage.setItem("tareas", JSON.stringify(this.tareas))
      }
  },
// permite mostrar el item una ves es crado y no antes, e otras palabras hasta que no tome un valor el array no va a mostrarse    
  created () {
    this.tareas = JSON.parse(localStorage.getItem('tareas')) || []//por eso es get<<<<
  }    
}
</script>

<style lang="scss">
@import './sass/main.scss';
    #col h1 {
        text-align: center;
        color: #00d1b2;
    }
    #col h5 {
        text-align: center;
        margin-top: 20px;
    }
    #tareas h1{
        background-color: aquamarine;
    }
    #title h1 {
        text-align: center;
        color: #00d1b2;
        font-weight: 800;
    }
    h1 {
        font-size: 30px;
    }
    h5 {
        font-size: 20px;
    }
    #input p {
        font-size: 18px;
        font-weight: 800;
        color: red;
        margin-top: 10px;
    }
    .control {
        margin-top: 10px;
    }
    .divider {
        margin-top: 20px;
        margin-bottom: 20px;
        height: 2px;
        overflow: hidden;
        background-color: black;
    }
    textarea {
        margin-top: 10px;
    }
</style>
