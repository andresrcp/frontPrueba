<template>
  <div class="container">
    <div class="row">
      <form @submit.prevent="agregarUsuario">
        <div class="col m12 card-panel">
          <div class="col m4">
            <label for="nombre">Nombre</label>
            <input type="text" name="nombre" id="nombre" v-model="nombre">
          </div>
          <div class="col m4">
            <label for="apellido">Apellido</label>
            <input type="text" name="apellido" id="apellido" v-model="apellido">
          </div>
        </div>

        <div class="row">
          <div class="col m3">
            <label for="edad">edad</label>
            <input type="number" name="edad" id="edad" v-model="edad">
          </div>
          <div class="col m4">
            <label for="estadoCivil">
              <select name="estadoCivil" id="estadocivil" v-model="estadoCivil">
                <option value="">Selecione</option>
                <option value="C">Casado</option>
                <option value="S">Soltero</option>
                <option value="D">Divorciado</option>
                <option value="V">Viudo</option>
              </select>
            </label>
          </div>
          <div class="col m4">
            <label for="edad">correo</label>
            <input type="email" name="correo" id="correo" v-model="correo">
          </div>
        </div>

        <div class="row">
          <form @submit.prevent="agregarPasatiempo">
            <div class="col m4 card-panel">
              <label for="pasatiempo">Pasatiempo</label>
              <input type="text" name="pasatiempo" id="pasatiempo" v-model="pasatiempo">
              <button type="submit" class="btn indigo darken-4">Agregar Pasatiempo <i
                  class="material-icons right">add_box</i></button>
              <ul>
                <li v-for="pasatiempo in pasatiempos" v-bind:key="pasatiempo">{{pasatiempo.id}} - {{ pasatiempo.descripcion }}</li>
              </ul>
            </div>
          </form>
        </div>

        <div class="row">
          <div class="col m4">
            <label for="suscribirse">
              <input type="checkbox" name="suscribirse" id="suscribirse" v-model="suscribirse">
              <span>Suscribirse al boletin de noticias</span>
            </label>
          </div>
        </div>

        <div class="row">
          <button type="submit" class="btn indigo darken-4">
            Agregar Usuario
            <i class="material-icons right">
              add_circle
            </i>
          </button>
        </div>
      </form>
    </div>
  </div>

  <div class="container">
    <div class="row">
      <div class="col m12">
        <table class="table bordered striped">
          <thead>
            <tr>
              <th>Nombre</th>
              <th>Apellido</th>
              <th>Edad</th>
              <th>Estado Civil</th>
              <th>Correo</th>
              <th>Pasatiempos</th>
              <th>Suscrito</th>
              <th>Editar</th>
              <th>Eliminar</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="usuario in usuarios" v-bind:key="usuario">
              <td>{{ usuario.nombre }}</td>
              <td>{{ usuario.apellido }}</td>
              <td>{{ usuario.edad }}</td>
              <td>{{ usuario.estadoCivil }}</td>
              <td>{{ usuario.correo }}</td>
              <td>
                <ul>
                  <li v-for="pasatiempo in usuario.pasatiempos" v-bind:key="pasatiempo">{{ pasatiempo.id }} -
                    {{ pasatiempo.descripcion }}</li>
                </ul>
              </td>
              <td>
                <label for="suscrito">
                  <span>
                    <input type="checkbox" name="suscrito" id="suscrito" disabled v-model="usuario.suscribirse">
                  </span>
                </label>
              </td>
              <td>
                <a href="#!">
                  <i class="material-icons">create</i>
                </a>
              </td>
              <td>
                <a href="#!">
                  <i class="material-icons">delete</i>
                </a>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import M from 'materialize-css'


export default {
  name: 'App',
  data() {
    return {
      nombre: '',
      apellido: '',
      edad: 0,
      estadoCivil: '',
      documento: '',
      pasatiempo: '',
      pasatiempos: [],
      suscribirse: false,
      correo: '',

      usuarios: [],

      selectInstances: []
    }
  },

  mounted() {
    var elements = document.querySelectorAll('select');
    this.selectInstances = M.FormSelect.init(elements, null);
  },

  methods: {
    agregarUsuario() {
      var data = {
        nombre: this.nombre,
        apellido: this.apellido,
        edad: this.edad,
        estadoCivil: this.estadoCivil,
        documento: this.documento,
        pasatiempos: this.pasatiempos,
        suscrito: this.suscribirse,
        correo: this.correo,
      };
      this.usuarios.push(data);
      this.nombre = '';
      this.apellido = '';
      this.edad = '';
      this.estadoCivil = '';
      this.documento = '';
      this.pasatiempos = [];
      this.suscribirse = false;
      this.correo = '';
    },
    agregarPasatiempo(){
        var total = this.pasatiempos.length;
        var ultimo = 0;
        if (total > 0){
          ultimo = this.pasatiempos[total - 1].id;
        }
        var data = {
          id : ultimo+1,
          descripcion : this.pasatiempo
        }
        this.pasatiempos.push(data);
        this.pasatiempo = '';
    }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
