<template>
  <v-app>
    <v-app-bar
      app
      flat
    >
      <v-container class="py-0 fill-height">
        <v-toolbar-title>Илонус</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-title>О нас</v-toolbar-title>
      </v-container>
    </v-app-bar>
    <v-main>
      <v-layout row>
        <v-col cols="4" md="2">
          <router-link to="/"><v-btn text>Главная</v-btn></router-link><br>
          <router-link to="/about"><v-btn text>О нас</v-btn></router-link><br>
          <router-link to="/gallery"><v-btn text>Галерея</v-btn></router-link>
          <v-card>
            Зарегистрировано погодных событий:
          </v-card>
        </v-col>
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
export default {
  name: "AboutPage",
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
        console.log(data)
      })
  }
}
</script>

<style scoped>

</style>
