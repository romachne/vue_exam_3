<template>
  <v-app>
    <header-bar />
    <v-main>
      <v-layout row>
        <nav-bar />
        <v-col cols="20" md="10">
          <p>
            {{data.text}}
          </p>
        </v-col>
      </v-layout>
    </v-main>
  </v-app>

</template>

<script>
import NavBar from "@/components/NavBar";
import HeaderBar from "@/components/HeaderBar";
export default {
  name: "AboutPage",
  components: {HeaderBar, NavBar},
  data () {
    return {
      data: []
    }
  },
  mounted () {
    fetch("https://demo-api.vsdev.space/api/elonus/about_page")
      .then(response => response.json())
      .then(data => {
        this.data = data
      })
  }
}
</script>

<style scoped>

</style>
