<template lang="html">
  <ul v-if="films" id="films-list">
    <films-list-item v-for="(film, index) in films" v-bind:key="index" v-bind:film="film"></films-list-item>
  </ul>
</template>

<script>
import FilmsListItem from './FilmsListItem.vue';
export default {
  name: 'films-list',
  props: ['films'],
  components: {
    'films-list-item': FilmsListItem
  }
}
</script>

<style lang="css" scoped>
 #films-list {
   width: 500px;
   border: 1px black solid;
 }
</style>
