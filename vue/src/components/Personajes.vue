<script>
import axios from 'axios'
let API_URL = `https://rickandmortyapi.com/api/character`
export default {
  data() {
    return {
      info: [],
      personajes: [],
      cont:2
    }
  },
  mounted() {
    axios.get(API_URL)
      .then((response) => {
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
  },
  methods: {
    pag(num) {
      API_URL='https://rickandmortyapi.com/api/character/?page='+num
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
      this.cont++
    }
  },
}
</script>

<template>
    <br>
  <h2>Hay {{ info.count }} personajes en el programa de Rick & Morty</h2>
  <br>
  <button @click="pag(cont)">página {{ cont }}</button>
  <br>
  <ul>
    <br>
    <li class="text-center" v-for="p in personajes">
        <img v-bind:src="p.image"  alt="no image">
        <a >{{ p.name }} 
        <br>  id:{{ p.id }}
        <br> status:{{ p.status }} 
        <br> species:{{ p.species }} 
        <br> type:{{ p.type }} 
        <br> gender:{{ p.gender }} 
        </a>
    </li>
  </ul>
</template>