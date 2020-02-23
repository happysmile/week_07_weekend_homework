<template lang="html">
  <li>{{person.name}}</li>
</template>

<script>
export default {
  name: 'people-list-item',
  props: ['person']
}
</script>

<style lang="css" scoped>
</style>
