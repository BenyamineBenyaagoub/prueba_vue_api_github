<template>
<div>
    <Navbar></Navbar>

  <div class="container mt-4" id="mi-componente" >
    <h1>Consultar Perfiles</h1>
  

    <label for="feedback-user">Nombre de usuario</label>

    <b-input-group class="mt-3">
      <b-form-input
        v-model="search"
        :state="validation"
        v-on:keyup.enter="searchData"
        id="feedback-user"
      ></b-form-input>
      <b-input-group-append>
        <b-button v-on:click="searchData"  variant="outline-success">
          <fa icon="search" /> Buscar
        </b-button>
      </b-input-group-append>
    </b-input-group>

    <b-form-invalid-feedback :state="validation">
      El nombre debe tener mas de 4 carácteres y no puede ser "Logitravel"
    </b-form-invalid-feedback>

    <div class="row">
      <Usuarios
        @showProfile="showProfile"
        v-for="perfil of perfiles.slice(0, 10)"
        v-bind:key="perfil.id"
        v-bind:perfil="perfil"
      />

      <Usuario v-bind:perfil="perfil" v-bind:modal="modal" />
    </div>
  </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Usuario from "./components/Usuario.vue";
import Usuarios from "./components/Usuarios.vue";
import axios from "axios";

export default {
  name: 'App',
  components: {
    Navbar,
    Usuarios,
    Usuario,
  },
  data: function () {
    return {
      perfiles: [],
      search: "",
      modal: false,
      perfil: {},
    };
  },
  computed: {
    validation() {
      return (
        this.search.length > 4 && this.search.toLowerCase() != "logitravel"
      );
    },
  },
  methods: {
    fetch() {
      let result = axios
        .get("https://api.github.com/search/users?q=" + this.search)

        .then((res) => {
          this.perfiles = res.data.items;
          console.log(res.data);
        })

        .catch((err) => {
          err;
          console.log(err);
        });

      result;
    },

    searchData() {
      this.modal= false;
      this.fetch();
    },

    showProfile(user) {
      this.fetchOne(user);
    },

    async fetchOne(user) {
      let result = await axios.get(`https://api.github.com/users/${user}`);
      this.perfil = result.data;
      this.modal = true;
      console.log(this.perfil);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
