<template>
  <v-app id="inspire">
  <v-navigation-drawer
  v-model="drawer"
  :mobile-breakpoint="768"
  app
  >
      <v-img
      class="pa-4 pt-7"
      src="mountains-gb3dd8e94f_1280.jpg"
      :height="$route.path === '/' ? '240' : '170'"
        gradient="to top right, rgba(100,115,201,.7), rgba(25,32,72,.7)"
    > <v-avatar size="70" class="mb-2">
      <img
        src="https://media-exp2.licdn.com/dms/image/C4D03AQHxT2CsTeTMYA/profile-displayphoto-shrink_200_200/0/1597182038657?e=1661990400&v=beta&t=FxfXTRW8-Cda1GY0K_kTXEW0FORm1Ex4wkni_vuirj4"
        alt="John"
      >
    </v-avatar>
    <div class="white--text text-subtitle-1 font-weight-bold">Ekrem Arslan</div>
    <div class="white--text text-subtitle-2">ekodestek@gmail.com</div>
    </v-img>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
<v-app-bar
      app
      absolute
      color="primary"
      dark
      shrink-on-scroll
      prominent
      src="mountains-gb3dd8e94f_1280.jpg"
      permanent
      :height="$route.path === '/' ? '240' : '170'"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(100,115,201,.9), rgba(25,32,72,.7)"
        ></v-img>
      </template>

        <v-container class="header-continer pa-0">
          <v-row>
            <v-app-bar-nav-icon  @click="drawer =!drawer"></v-app-bar-nav-icon> 
            <v-spacer></v-spacer>
            <search />
          </v-row>
          <v-row>
            <v-app-bar-title class="text-h4 ml-4">{{ $store.state.appTitle }}</v-app-bar-title>
          </v-row>
          <v-row>
            <live-date-time />
          </v-row>
          <v-row v-if="$route.path === '/'">
            <field-add-task />
          </v-row>
        </v-container>

    </v-app-bar>
    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import Search from '@/components/Tools/Search.vue'
export default {
  data: () => ({ 
    drawer: null,
    items: [
      { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
      { title: 'About', icon: 'mdi-help-box', to: '/about' },
    ],
    right: null, 
  }),
  components:{
    'field-add-task' : require('@/components/Todo/AddTask.vue').default,
    'snackbar' : require('@/components/Shared/Snackbar.vue').default,
    'search' : require('@/components/Tools/Search.vue').default,
    'live-date-time' : require('@/components/Tools/LiveDateTime.vue').default
  },
  mounted() {
    this.$store.dispatch('getTasks')
  }
}
</script>

<style lang="sass">
  .header-container
    max-width: none !important
</style>