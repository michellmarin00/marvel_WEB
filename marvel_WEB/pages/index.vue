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

          <v-card-text>Nombre del personaje= {{ personaje.name }}</v-card-text>
          <v-card-text>Descripción= {{ personaje.description }}</v-card-text>
          <v-row class="d-flex" justify="center">
            <v-card-text>Comics= {{ personaje.comics.available }}</v-card-text>
            <v-card-text >Events= {{ personaje.events.available }}</v-card-text>
            <v-card-text >Stories= {{ personaje.stories.available }}</v-card-text>
            <v-card-text>Series= {{ personaje.series.available }}</v-card-text>
          </v-row>

          <v-divider></v-divider>
          <v-card-subtitle>
            Nombre de las 3 primeras series:
            <br />
          </v-card-subtitle>
          <br />

          <v-card-text v-for="item in personaje.series.items.slice(0, 3)" :key="item">
            {{ item.name }}
          </v-card-text>

          <div v-for="serie in series" :key="serie.id">
            <v-expand-transition>
              <div v-show="personaje.id === sele">
                <v-card-text> </v-card-text>
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
      id: ' ',
      sele: null,
      series: [],
    }
  },

  methods: {
    getId(id) {
      this.$id = id
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
