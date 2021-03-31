<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Pilot-App</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content>
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>
      <div id="container">
          <h2>Liten testapp för att se vad som skiljer i NativeScript och Ionic utan att använda någon av mobilens funktioner</h2>
          <p>Genom att klicka på knappen startas en timer mellan 3-6 sekunder som ska klickas på så fort som möjligt</p>
            <button @click="start" :disabled="isStarted">Starta timer</button>
            <button @click="loadElements" :disabled="isStarted">Ladda element</button>
          
            <Clicker v-if="isStarted" :delay="delay" @reactionTime="result"></Clicker>
            <Result v-if="showResult" :time="time"></Result>
         
            <ul v-if="fillers.length">
              <!-- <li v-for="filler in fillers" :key="filler.id"></li> -->
          
              <Filler v-for="filler in fillers" :key="filler.id" :joke="filler.joke"></Filler>
            
            </ul>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import Clicker from '../components/Clicker.vue';
import Filler from '../components/Filler.vue';
import Result from '../components/Result.vue';

export default defineComponent({
  name: 'Home',
  components: {
    Clicker,
    Filler,
    Result,
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar
  },
  data(){
    return {
      isStarted: false,
      delay: null,
      time: 32,
      showResult: true,
      fillers: []
    }
  },
  methods: {
    start() {
      this.delay = Math.floor(3000 + Math.random() * 3000)
      this.isStarted = true
      this.showResult = false
    },
    result(time) {
      this.time = time
      this.isStarted = false
      this.showResult = true
    },
    loadElements() {
      fetch('http://api.icndb.com/jokes/random/25')
      .then(resp => resp.json())
      .then(json => this.fillers = json.value)
      .catch(err => console.log('Error: ' + err.message))
    }
  },
  mounted() {

  }
});
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  /* top: 10%;
  transform: translateY(-10%); */
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}

ion-toolbar {
  --background:#2c3e50;
}
ion-title {
  color: #e65a33;
  text-align: center;
}

body {
  margin: 0;
  padding: 0;
}
ul {
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
h1 {
  color: #e65a33;
  background:#2c3e50;
  padding: 20px;
}
h2 {
  width: 480px;
  text-align: center;
  margin: 10px auto;
}
button {
  background: #2c3e50;
  color: #e65a33;
  border: none;
  padding: 14px 28px;
  border-radius: 4px;
  font-size: 20px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>