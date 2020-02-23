<template lang="html">
  <div id="app">
    <search-film v-bind:films="films"
    v-bind:people="people"
    v-bind:locations="locations"
    v-bind:species="species"
    v-bind:vehicles="vehicles"></search-film>
    <div class="film-list">
      <films-list v-if="filmSearching" v-bind:films="filteredFilms"></films-list>
      <films-list v-else-if="films.length>0" v-bind:films="films"></films-list>
      <film-details v-if="selectedFilm"
      v-bind:film="selectedFilm"
      v-bind:people="peopleInSelectedFilm"
      v-bind:locations="locationsInSelectedFilm"
      v-bind:species="speciesInSelectedFilm"
      v-bind:vehicles="vehiclesInSelectedFilm"></film-details>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';
import FilmsList from './components/FilmsList.vue';
import FilmDetails from './components/FilmDetails.vue';
import SearchFilm from './components/SearchFilm.vue';
export default {
  name: "app",
  data(){
    return {
      films: [],
      selectedFilm: null,
      filteredFilms: [],
      filmSearching: false,
      people: [],
      locations: [],
      species: [],
      vehicles: []
    }
  },
  computed: {
    peopleInSelectedFilm: function () {
      if(this.selectedFilm!=null){
        return this.people.filter((person) => person.films.includes(this.selectedFilm.url));
      }
    },
    locationsInSelectedFilm: function(){
      if(this.selectedFilm!=null){
        return this.locations.filter((location) => location.films.includes(this.selectedFilm.url));
      }
    },
    speciesInSelectedFilm: function(){
      if(this.selectedFilm!=null){
        return this.species.filter((specie) => specie.films.includes(this.selectedFilm.url));
      }
    },
    vehiclesInSelectedFilm: function(){
      if(this.selectedFilm!=null){
        return this.vehicles.filter((vehicle) => vehicle.films.includes(this.selectedFilm.url));
      }
    }
  },
  components: {
    'films-list': FilmsList,
    'film-details': FilmDetails,
    'search-film': SearchFilm
  },
  mounted(){
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(res => res.json())
    .then(films => this.films = films)

    fetch('https://ghibliapi.herokuapp.com/people')
    .then(res => res.json())
    .then(people => this.people = people)

    fetch('https://ghibliapi.herokuapp.com/locations')
    .then(res => res.json())
    .then(locations => this.locations = locations)

    fetch('https://ghibliapi.herokuapp.com/species')
    .then(res => res.json())
    .then(species => this.species = species)

    fetch('https://ghibliapi.herokuapp.com/vehicles')
    .then(res => res.json())
    .then(vehicles => this.vehicles = vehicles)

    eventBus.$on('film-selected', (film) => {
      this.selectedFilm = film;
    })

    eventBus.$on('film-searched', (films) => {
      this.selectedFilm = null;
      this.filmSearching = true;
      this.filteredFilms = films;
    })

  }
}
</script>

<style lang="css" scoped>
  #app {
    font-family: Verdana, Arial, sans-serif;
  }

  #app .film-list {
    display: flex;
  }
</style>
