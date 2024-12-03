<template>
    <div id="app">

      <Buscador @search="buscarId"></Buscador>
      <Personaje :lista_personajes="personajes"/>

    </div>
</template>

<script>
  import axios from 'axios'
  import Personaje from './components/PersonajePoke.vue'
  import Buscador from './components/BuscadorPoke.vue'

  export default{
    name: 'App',
    components: {
      Personaje,
      Buscador
    },
    data: function (){
      return {
        personajes: [],
        personaje2: [],
      }
    },
    methods: {
      getPersonajes(){
        axios.get(`https://pokeapi.co/api/v2/pokemon/`)
        .then((resp)=> {
          console.log(resp.data)
          this.personajes = resp.data.results
          this.personaje2 = resp.data.results
        }).catch(e =>
          console.log(e)
        )
      },

      buscarId(ide) { // Aquí cambiamos "buscarID" por "buscarId"
      if (ide.length === 0) {
        // Si no hay ID, podemos restablecer la lista completa
        this.personajes = this.personaje2;
      } else {
        // Filtramos la lista de personajes según el ID
        this.personajes = this.personaje2.filter(item => item.id === parseInt(ide));
      }
    }
  },
    // ya existe un objeto en javascript pero aun no lo puede ver el usuario
    created() {
      this.getPersonajes() // llamo a la Api de donde se obtienen los personajes 
    }

  }
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
