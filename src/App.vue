<template>
  <div id="app">
    <v-container>
      <v-row align-content="center">
        <v-col align-self="center" cols="4">
          <v-text-field v-model="name"/>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-btn outlined @click="pesquisar">Pesquisar</v-btn>
        </v-col>
      </v-row>
      <div v-if="pokemon">
        <v-row>
          <v-img  max-height="100" max-width="100" :src="pokemon.image" />
        </v-row>
        <v-row>
          <ul class="text-left">
            <li v-for="ability in pokemon.abilities" :key="ability">
              {{ ability }}
            </li>
          </ul>
        </v-row>    
      </div>
      <div v-if="message">
        <v-row>
          <span>{{ message }}</span>
        </v-row>
      </div>  
    </v-container>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',

  data() {
    return {
      name: '',
      pokemon: null,
      message: null
    }
  },
  methods: {
    async pesquisar() {
      const url = `http://localhost:3000/pokemon?name=${this.name}`

      try {
        const { data } = await axios.get(url)
        this.pokemon = data
      }
      catch(e) {
        this.message = 'Não consta pokemon com este nome.'
      }
    }
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
