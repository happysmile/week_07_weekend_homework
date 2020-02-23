<template lang="html">
  <li v-on:click="showDetails">{{film.title}}</li>
</template>


<script>

import {eventBus} from '../main.js';

export default {
  name: 'films-list-item',
  props: ['film'],
  methods: {
      showDetails(){
      eventBus.$emit('film-selected', this.film)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
