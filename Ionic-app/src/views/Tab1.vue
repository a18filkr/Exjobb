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
            <ion-button size="large" expand="block" @click="loadCountries" :disabled="isLoaded">Ladda länder (webb api)</ion-button>
          </ion-col>
          <ion-col size-md="3"></ion-col>
        </ion-row>
        <ion-row>
          <ion-col size-md="3"></ion-col>
          <ion-col size-md="6">
            <ion-button size="large" expand="block" @click="loadVaccinations" :disabled="isLoaded">Ladda vaccinlista (lokal)</ion-button>
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
        <ion-row v-if="listobjects.length">
          <ion-col size-md="3"></ion-col>
          <ion-col size-md="6">
          <ion-list v-if="listobjects.length < 1000" mode="md">
            <!-- <Country v-for="listobject in listobjects" :key="listobject.id" :name="listobject.name"/> -->
            <ion-item v-for="listobject in listobjects" :key="listobject.Denominator">
              <ion-label>
                {{ listobject.name }}
              </ion-label>
            </ion-item>
          </ion-list>
          <ion-list v-if="listobjects.length > 1000" mode="md">
            <!-- <Country v-for="listobject in listobjects" :key="listobject.Denominator" :name="listobject.Region"/> -->
            <ion-item v-for="listobject in listobjects" :key="listobject.Denominator">
              <ion-label>
                {{ listobject.Region }}
              </ion-label>
            </ion-item>
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
// import Country from '../components/Country.vue';

export default ({
  name: 'Tab1',
  components: { ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonGrid, IonRow, IonButton, IonList, IonCol },
  data() {
    return {
      isLoaded: "false",
      isDeleted: "true",
      listobjects: []
    };
  },
  methods: {
    loadCountries() {
      fetch('https://restcountries.eu/rest/v2/all')
      .then(resp => resp.json())
      .then(json => this.listobjects = json)
      .catch(err => console.log('Error: ' + err.message))
      this.isLoaded = true
      this.isDeleted = false
    },
    loadVaccinations() {
      fetch("../../assets/json/covid-vaccin.json")
      .then(resp => resp.json())
      .then(json => {
        this.listobjects = json.records
        this.listobjects.splice(10000, this.listobjects.length)
        })
      .catch(err => console.log('Error: ' + err.message))
      this.isLoaded = true
      this.isDeleted = false
    },
    deleteElements() {
      this.listobjects.splice(0, this.listobjects.length)
      this.isLoaded = false
      this.isDeleted = true
    }
  }
})

</script>