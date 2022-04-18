<template>
  <v-app>
    <header-bar />
    <v-main>
      <v-layout row>
        <nav-bar />
        <v-col cols="10" md="5">
          <p>
            {{data.text}}
          </p>
        </v-col>
        <v-col cols="10" md="5">
          <v-img :src="data.image" alt=""></v-img>
        </v-col>
      </v-layout>


    </v-main>
  </v-app>

</template>

<script>
import NavBar from "@/components/NavBar";
import HeaderBar from "@/components/HeaderBar";
export default {
  name: "MainPage",
  components: {HeaderBar, NavBar},
  data () {
    return {
      data: []
    }
  },
  mounted () {
    fetch("https://demo-api.vsdev.space/api/elonus/home_page")
      .then(response => response.json())
      .then(data => {
        this.data = data
        console.log(data)
      })
  }
}
</script>

<style scoped>

</style>
