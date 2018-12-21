<template>
  <v-app>
    <v-toolbar color="primary white--text">
      <v-toolbar-title class="subtitle text-uppercase">
        <span>Spread</span>
        <span class="font-weight-light">sheets</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>

    <v-content>
      <v-container>
        <router-view></router-view>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      //
    }
  }
}
</script>
