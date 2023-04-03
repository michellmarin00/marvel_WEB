<template>
  <div>
    <div v-for="personaje in personajes" :key="personaje.id">
      <p>{{ personaje.name }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'IndexPage',

  data() {
    return {
      personajes: [],
    }
  },
  created() {
    const url = 'http://gateway.marvel.com/v1/public/characters?ts=8&apikey=59b68dc533d0551b400ee83dec5fd034&hash=0bc5896cc41eb4f0e51851bdbf8f2c2e'

    axios
      .get(url)
      .then((response) => (this.personajes = response.data.data.results))
  },
}
</script>
