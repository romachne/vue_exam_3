<template>
  <v-col cols="4" md="2">
    <router-link to="/"><v-btn text>Главная</v-btn></router-link><br>
    <router-link to="/about"><v-btn text>О нас</v-btn></router-link><br>
    <router-link to="/events"><v-btn text>События</v-btn></router-link>
    <v-card>
      Зарегистрировано погодных событий: {{data.events}}
      <img src="../assets/left_widget_img.jpg" alt="">
    </v-card>
  </v-col>
</template>

<script>
export default {
  name: "NavBar",
  data () {
    return {
      data: []
    }
  },
  mounted () {
    fetch("https://demo-api.vsdev.space/api/elonus/left_widget")
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
