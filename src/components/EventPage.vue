<template>
  <v-app>
    <header-bar />
    <v-main>
      <v-layout row>
        <nav-bar />
        <v-dialog
          v-model="dialog"
          persistent
          max-width="600px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              v-bind="attrs"
              v-on="on"
            >
              Открыть форму
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">Новое событие</span>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-form>
                  <v-text-field
                    v-model="picker"
                    :label="formdata.fields.date.title"
                  ></v-text-field>
                  <v-select
                    v-model="type"
                    :items="formdata.fields.type.values"
                    :label="formdata.fields.type.title"
                  >
                  </v-select>
                  <v-text-field
                    v-model="victims"
                    :label="formdata.fields.victims.title"
                  >
                  </v-text-field>
                </v-form>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="dialog = false"
              >
                Закрыть
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="submitForm()"
              >
                Сохранить
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-row>
          <v-col
            v-for="event in data"
            :key="event.id"
            cols="3"
          >
            <v-card
            >
              <v-card-title>{{event.type}}</v-card-title>
              <v-card-text>
                <p>{{event.date}}</p>
                <p>{{event.victims}}</p>
                <p>{{event.acid_power}}</p>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-layout>
    </v-main>
  </v-app>
</template>

<script>
import HeaderBar from "@/components/HeaderBar";
import NavBar from "@/components/NavBar";
import axios from "axios";
export default {
  name: "EventPage",
  components: {NavBar, HeaderBar},
  data () {
    return {
      data: [],
      formdata: [],
      dialog: '',
      victims: '',
      type: '',
      picker: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
    }
  },
  methods: {
    submitForm() {
      let formdata = { id: 141, type: this.type, date: this.picker, victims: this.victims, wind_speed: '3'}
      console.log(formdata)
      axios.post('https://demo-api.vsdev.space/api/elonus/events', formdata).catch(error => {
        this.errors = error.response.data.errors
        console.log("Errors= " + this.errors)
      })
      // this.data.push(formdata)
    }
  },
  mounted () {
    fetch("https://demo-api.vsdev.space/api/elonus/events")
      .then(response => response.json())
      .then(data => {
        this.data = data
        console.log(data)
      });
    fetch("https://demo-api.vsdev.space/api/elonus/events/form")
      .then(response => response.json())
      .then(data => {
        this.formdata = data
        console.log(data)
      })
  }
}
</script>

<style scoped>

</style>
