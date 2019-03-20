<template>
  <v-app :dark="dark">
    <v-toolbar app>
      <ul>
        <li>
          <v-toolbar-title class="headline text-uppercase">
            <span>Music</span>
            <span class="font-weight-light">Town</span>
          </v-toolbar-title>
        </li>
        <li><h6>Records</h6></li>
      </ul>
      <v-spacer></v-spacer>
      <v-btn
        flat
        @click.stop="changeTheme()"
      >
        <span class="mr-2">change theme</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <router-view />
    </v-content>

  </v-app>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data () {
    return {
      theme: true,
      dark: false
    }
  },
  methods:{
    changeTheme(){
      if (this.theme) {
        this.dark = true
        return this.theme = false
      } else {
        this.dark = false
        return   this.theme = true
      }
    }
  }
};
</script>

<style>

</style>
