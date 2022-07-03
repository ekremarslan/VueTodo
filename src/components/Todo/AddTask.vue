<template>
  <v-text-field
    v-model="newTaskTitle"
    @click:append="addTask"
    @keyup.enter="addTask"
    class="field-add-task pa-3"
    outlined
    placeholder="Add Task"
    append-icon="mdi-plus"
    hide-details
    clearable
  >
   <template v-slot:append>
      <v-icon
      @click="addTask"
      color="primary"
      :disabled="newTaskTitleInvalid"
      >
        mdi-plus
      </v-icon>
  </template>
            
  </v-text-field>
</template>

<script>
export default {
     data() {
        return {
            newTaskTitle: '',
        }
    },
    computed: {
      newTaskTitleInvalid(){
         return !this.newTaskTitle || this.newTaskTitle.startsWith(' ')
      }
    },
    methods: {
        addTask() {
          if(!this.newTaskTitleInvalid){
            this.$store.dispatch('addTask', this.newTaskTitle)
            this.newTaskTitle = ''
          }
        }
    },
};
</script>


<style lang="sass">
  .field-add-task.v-input--is-focused
    .v-input__slot
      background: rgba(31,94,120,0.5) !important

</style>
