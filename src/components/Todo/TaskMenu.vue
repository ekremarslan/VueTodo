<template>
<div>
  <v-menu bottom left>
    <template v-slot:activator="{ on, attrs }">
      <v-btn color="primary" icon v-bind="attrs" v-on="on">
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </template>
    <v-list>
      <v-list-item 
      v-for="(item, index) in items" 
      :key="index"
      @click="handleClick(index)"
      >
        <v-list-item-icon>
          <v-icon v-text="item.icon"></v-icon>
        </v-list-item-icon>
        <v-list-item-title>{{ item.title }}</v-list-item-title>
      </v-list-item>
    </v-list>
  </v-menu>

 <dialog-edit 
  v-if="dialogs.edit" 
  @close="dialogs.edit = false"
  :task="task" />
    
<dialog-delete 
  v-if="dialogs.delete" 
  @close="dialogs.delete = false"
  :task="task" />

<dialog-duedate
  v-if="dialogs.duedate" 
  @close="dialogs.duedate = false"
  :task="task" />

</div>

</template>

<script>
export default {
  props: ['task'],
  components: {
    "dialog-delete": require("@/components/Todo/Dialogs/DialogDelete.vue").default,
    "dialog-edit": require("@/components/Todo/Dialogs/DialogEdit.vue").default,
    "dialog-duedate": require("@/components/Todo/Dialogs/DialogDueDate.vue").default,
  },
  data: () => ({
    items: [
      { title: "Edit", icon: "mdi-pencil" ,click() {  this.dialogs.edit = true } },
      { title: "Due Date", icon: "mdi-calendar" ,click() { this.dialogs.duedate = true } },
      { title: "Delete", icon: "mdi-delete", click() { this.dialogs.delete = true } },
      { title: "Sort", icon: "mdi-drag-horizontal-variant", 
      click() { 
          if(!this.$store.state.search){
            this.$store.commit('sortingToggle') 
          } 
          else {
            this.$store.commit('showSnackbar', 'Snackbar Message!') 
          }
        } 
      }
    ],
    dialogs: {
      delete: false,
      edit: false,
      duedate: false
    }
  }),    
  methods: {
    handleClick(index) {
      this.items[index].click.call(this)
    }
  }
}
</script>

<style>
</style>