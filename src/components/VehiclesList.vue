<template lang="html">
  <ul id="vehicles-list">
    <vehicles-list-item v-for="vehicle in vehicles" v-bind:vehicle="vehicle"></vehicles-list-item>
  </ul>
</template>

<script>
import VehiclesListItem from './VehiclesListItem.vue';
export default {
  name: 'vehicles-list',
  props: ['vehicles'],
  components: {
    'vehicles-list-item': VehiclesListItem
  }
}
</script>

<style lang="css" scoped>
</style>
