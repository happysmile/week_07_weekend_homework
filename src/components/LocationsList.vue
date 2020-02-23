<template lang="html">
  <ul id="locations-list">
    <locations-list-item v-for="location in locations" v-bind:location="location"></locations-list-item>
  </ul>
</template>

<script>
import LocationsListItem from './LocationsListItem.vue';
export default {
  name: 'locations-list',
  props: ['locations'],
  components: {
    'locations-list-item': LocationsListItem
  }
}
</script>

<style lang="css" scoped>
</style>
