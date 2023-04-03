<template>
  <v-app>
    <div>
      <v-container v-for="personaje in personajes" :key="personaje.id">
        <v-card>
          <v-img
            :src="
              personaje.thumbnail.path + '.' + personaje.thumbnail.extension
            "
          >
          </v-img>

          <p>nombre {{ personaje.name }}</p>
          <p>{{ personaje.description }}</p>
          <p> comics {{ personaje.comics.available }} </p>
          <p>events {{ personaje.events.available }}</p>
          <p>stories {{ personaje.stories.available }}</p>
          <p>series {{ personaje.series.available }}</p>

          <v-btn @click="getId(personaje.id); sele=personaje.id"> ver </v-btn>

          <div v-for="serie in series" :key="serie.id">

          <v-expand-transition> 
            <div v-show="personaje.id===sele">
              <v-card-text>
              </v-card-text>
            </div>
          </v-expand-transition>

          </div>

        </v-card>
      </v-container>
    </div>
  </v-app>
</template>

<script>
import axios from 'axios'

export default {
  name: 'IndexPage',

  data() {
    return {
      personajes: [],
      id: " ",
      sele: null,
      series:[],
    }
  },

  methods:{
    getId(id){
      this.$id=id
    },
  },

  created() {
    const url =
      'http://gateway.marvel.com/v1/public/characters?ts=8&apikey=59b68dc533d0551b400ee83dec5fd034&hash=0bc5896cc41eb4f0e51851bdbf8f2c2e'
    let serieUrl =
      'http://gateway.marvel.com/v1/public/characters/' +
      `${this.id}` +
      '/series?ts=8&apikey=59b68dc533d0551b400ee83dec5fd034&hash=0bc5896cc41eb4f0e51851bdbf8f2c2e'
    axios
      .get(url)
      .then((response) => (this.personajes = response.data.data.results))

    axios
      .get(serieUrl)
      .then((response) => (this.series = response.data.data.results))
  },
}
</script>
