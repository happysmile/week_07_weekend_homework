<template lang="html">
  <div class="search-box">
    <select v-model="search.parameter">
      <option value="title" selected>Title</option>
      <option value="director">Director</option>
      <option value="people">Character</option>
      <option value="locations">Location</option>
      <option value="species">Species</option>
      <option value="vehicles">Vehicle</option>
    </select>
    <input type="text" v-on:input="filterFilms(films)" v-model="search.text" placeholder="Search film">
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: "search-film",
  props: ['films', 'people', 'vehicles', 'species', 'locations'],
  data(){
    return {
      "search": {
        results: [],
        parameter: 'title',
        text: "" }
    }
  },
  methods: {
    peoplePerFilm(film) {
      if(film.people!=null){
        return this.people.filter((person) => person.url.includes(film.people));
      }
    },
    locationsPerFilm(film) {
      if(film.locations!=null){
        return this.locations.filter((location) => location.url.includes(film.locations));
      }
    },
    speciesPerFilm(film) {
      if(film.species!=null){
        return this.species.filter((specie) => specie.url.includes(film.species));
      }
    },
    vehiclesPerFilm(film) {
      if(film.vehicles!=null){
        return this.vehicles.filter((vehicle) => vehicle.url.includes(film.vehicles));
      }
    },

    filterFilms(films) {
      // this.search.results = films.filter(film => film.title.toLowerCase().includes(this.search.text.toLowerCase()));
      // eventBus.$emit('film-searched', this.search.results);
      this.search.results = films.filter((film) => {
        // title and director search parameters are simple strings
        // but people, locations, species and vehicles are arrays!
        if(Array.isArray(film[this.search.parameter])){
          // the array items are urls of people, locations, vehicles and species
          // must be converted into strings of their names
          // then the search text can be matched
          let arrayToSearch = [];
          switch (this.search.parameter) {
            case "people":
              arrayToSearch =  this.peoplePerFilm(film);
              break;
            case "locations":
              arrayToSearch =  this.locationsPerFilm(film);
              break;
            case "species":
              arrayToSearch =  this.speciesPerFilm(film);
              break;
            case "vehicles":
              arrayToSearch =  this.vehiclesPerFilm(film);
              break;
          }
          const arrayOfLowerCaseNames = arrayToSearch.map((item) => item.name.toLowerCase());
          return arrayOfLowerCaseNames.includes(this.search.text.toLowerCase());
        } else {
          return film[this.search.parameter].toLowerCase().includes(this.search.text.toLowerCase());
        }
      });
      eventBus.$emit('film-searched', this.search.results);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
