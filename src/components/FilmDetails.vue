<template lang="html">
  <div class="film-details">
    <h2>{{film.title}}</h2>
    <p>{{film.description}}</p>
    <p>Director: {{film.director}}</p>
    <p>Producer: {{film.producer}}</p>
    <p>Release date: {{film.release_date}}</p>
    <div v-if="people.length>0">
      <p>People</p>
      <ul>
        <li v-for="person in people">{{person.name}}</li>
      </ul>
    </div>
    <div v-if="locations.length>0">
      <p>Locations</p>
      <ul>
        <li v-for="location in locations">{{location.name}}</li>
      </ul>
    </div>
    <div v-if="species.length>0">
      <p>Species</p>
      <ul>
        <li v-for="specie in species">{{specie.name}}</li>
      </ul>
    </div>
    <div  v-if="vehicles.length>0">
      <p>Vehicles</p>
      <ul>
        <li v-for="vehicle in vehicles">{{vehicle.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "film-details",
  props: ["film", "people", "locations", "species", "vehicles"]
}
</script>

<style lang="css" scoped>
  .film-details {
    width: 300px;
    border: 1px black solid;
  }
</style>
