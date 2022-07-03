<template>
  <v-btn 
  v-if="$store.state.sorting"
  @click="$store.commit('sortingToggle')"
  class="button-done-sorting"
  color="primary"
  >
    Done Sorting
  </v-btn>
</template>

<script>
export default {

}
</script>

<style lang=sass>
   .button-done-sorting
     position: fix
     bottom: 0px
     left: 50%
     transform: translateX(-50%)
</style>