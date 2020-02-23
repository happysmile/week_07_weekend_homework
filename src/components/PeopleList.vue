<template lang="html">
  <ul id="people-list">
    <people-list-item v-for="person in people" v-bind:person="person"></people-list-item>
  </ul>
</template>

<script>
import PeopleListItem from './PeopleListItem.vue';
export default {
  name: 'people-list',
  props: ['people'],
  components: {
    'people-list-item': PeopleListItem
  }
}
</script>

<style lang="css" scoped>
</style>
