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

          <h3 class="ml-4">Nombre del personaje: {{ personaje.name }}</h3>
          <br />
          <h4 class="ml-4" v-if="personaje.description !=='' ">Descripción= {{ personaje.description }}</h4>
          <h4 class="ml-4" v-else>Descripción= No existe descripción para este personaje.</h4>

          <br />
          <div >
            <p>Comics= {{ personaje.comics.available }}</p>
            <p>Events= {{ personaje.events.available }}</p>
            <p>Stories= {{ personaje.stories.available }}</p>
            <p>Series= {{ personaje.series.available }}</p>
          </div>

          <v-divider></v-divider>
          <h3 class="ml-4">
            Nombre de las 3 primeras series:
            <br />
        </h3>
          <br />

          <v-card-text v-for="item in personaje.series.items.slice(0, 3)" :key="item">
            {{ item.name }}
          </v-card-text>
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
    }
  },
  created() {
    const url =
      'http://gateway.marvel.com/v1/public/characters?ts=8&apikey=59b68dc533d0551b400ee83dec5fd034&hash=0bc5896cc41eb4f0e51851bdbf8f2c2e'
    
    axios
      .get(url)
      .then((response) => (this.personajes = response.data.data.results))
  },
}
</script>

 <style>
  p{margin-top: -20px; margin-left: 16px;}
</style>