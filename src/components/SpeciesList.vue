<template lang="html">
  <ul id="species-list">
    <species-list-item v-for="specie in species" v-bind:specie="specie"></species-list-item>
  </ul>
</template>

<script>
import SpeciesListItem from './SpeciesListItem.vue';
export default {
  name: 'species-list',
  props: ['species'],
  components: {
    'species-list-item': SpeciesListItem
  }
}
</script>

<style lang="css" scoped>
</style>
