<template>
    <Page>
        <ActionBar>
            <Label text="List Test"></Label>
        </ActionBar>
        <StackLayout orientation="vertical">
          <Label :text="message" textWrap="true" class="label-padding list-text"></Label>
          <Button @tap="loadCountries" :isEnabled="!isLoaded" text="Ladda länder(Webb)" padding="30"/>
          <Button @tap="loadVaccinations" :isEnabled="!isLoaded" text="Ladda vaccin(lokal)" padding="30"/>
          <Button @tap="deleteElements" :isEnabled="!isDeleted" text="Radera Lista" padding="30"/>
          <ListView v-if="listobjects.length" for="object in listobjects" height="90%">
            <v-template v-if="listobjects.length < 1000">
              <Label :text="object.name" class="label-padding"/>
            </v-template>
            <v-template v-if="listobjects.length > 1000">
              <Label :text="object.Region" class="label-padding"/>
            </v-template>
          </ListView>
        </StackLayout>

    </Page>
</template>

<script>
  import json from "../assets/json/covid-vaccin.json"

  export default {
    data() {
      return {
        listobjects: [],
        vaccinations: json,
        isLoaded: false,
        isDeleted: true,
        message: "Skapar en lista med länder och radera igen.",

      };
    },
    methods: {
    loadCountries() {
      fetch('https://restcountries.eu/rest/v2/all')
      .then(resp => resp.json())
      .then(json => this.listobjects = json)
      .catch(err => console.log('Error: ' + err.message))
      console.log(this.listobjects.length)
      this.isLoaded = true
      this.isDeleted = false
    },
    loadVaccinations() {
      // console.log(json.records)
      // fetch("json")
      // .then(resp => resp.json())
      // .then(json => this.listobjects = json.records)
      // .catch(err => console.log('Error: ' + err.message))
      this.listobjects = [...json.records]
      console.log(this.listobjects[0].Region)
      this.isLoaded = true
      this.isDeleted = false
    },
    deleteElements() {
      console.log(this.listobjects.length)
      this.listobjects.splice(0, this.listobjects.length)
      console.log(this.listobjects.length)
      this.isLoaded = false;
      this.isDeleted = true;
    },
    showRegion(e) {
      console.log(e.item.ReportingCountry)
    },
    showCountry(e) {
      console.log(e.item.name)
    }
    },

  };
</script>

<style scoped>

.label-padding {
  padding: 25px;
}

.list-text {
  margin: 10px auto;
  width: 580px;
  font-size: 18px;
  text-align: center;
}

</style>
