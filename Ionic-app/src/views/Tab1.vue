<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>List Test</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <ion-grid>
        <ion-row>
          <ion-col size-md="3"></ion-col>
          <ion-col size-md="6">
            <ExploreContainer name="List test" text="Skapa en lista med länder och radera igen."/>
          </ion-col>
          <ion-col size-md="3"></ion-col>
        </ion-row>
        <ion-row>
          <ion-col size-md="3"></ion-col>
          <ion-col size-md="6">
            <ion-button size="large" expand="block" @click="loadElements" :disabled="isLoaded">Ladda lista</ion-button>
          </ion-col>
          <ion-col size-md="3"></ion-col>
        </ion-row>
        <ion-row>
          <ion-col size-md="3"></ion-col>
          <ion-col size-md="6">
            <ion-button size="large" expand="block" @click="deleteElements" :disabled="isDeleted">Radera lista</ion-button>
          </ion-col>
          <ion-col size-md="3"></ion-col>
        </ion-row>
        <ion-row v-if="countries.length">
          <ion-col size-md="3"></ion-col>
          <ion-col size-md="6">
          <ion-list mode="md">
            <Country v-for="country in countries" :key="country.id" :name="country.name" :icon="country.flag"/>
          </ion-list>
          </ion-col>
          <ion-col size-md="3"></ion-col>

        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonRow, IonButton, IonList, IonCol } from '@ionic/vue';
import ExploreContainer from '../components/ExploreContainer.vue';
import Country from '../components/Country.vue';

export default ({
  name: 'Tab1',
  components: { Country, ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonGrid, IonRow, IonButton, IonList, IonCol },
  data() {
    return {
      isLoaded: "false",
      isDeleted: "true",
      countries: []
    };
  },
  methods: {
    loadElements() {
      fetch('https://restcountries.eu/rest/v2/all')
      .then(resp => resp.json())
      .then(json => this.countries = json)
      .catch(err => console.log('Error: ' + err.message))
      this.isLoaded = true
      this.isDeleted = false
    },
    deleteElements() {
      this.countries.splice(0, this.countries.length)
      this.isLoaded = false
      this.isDeleted = true
    }
  }
})

</script>