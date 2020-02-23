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
    <input type="text" v-on:input="filterFilms" v-model="search.text" placeholder="Search film">
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
      if(film.people.length>0){
        return this.people.filter((person) => film.people.includes(person.url));
      }
    },
    locationsPerFilm(film) {
      if(film.locations.length>0){
        return this.locations.filter((location) => film.locations.includes(location.url));
      }
    },
    speciesPerFilm(film) {
      if(film.species.length>0){
        return this.species.filter((specie) => film.species.includes(specie.url));
      }
    },
    vehiclesPerFilm(film) {
      if(film.vehicles.length>0){
        return this.vehicles.filter((vehicle) => film.vehicles.includes(vehicles.url));
      }
    },

    filterFilms() {
      this.search.results = this.films.filter((film) => {
        // film.title and film.director are simple strings
        // but film.people, film.locations, film.species and film.vehicles are arrays!
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
          return arrayOfLowerCaseNames.filter( (item) => item.includes(this.search.text.toLowerCase()));
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
