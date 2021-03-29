<template>
  <h1>Pilot-App</h1>
  <h2>Liten testapp för att se vad som skiljer i NativeScript och Ionic utan att använda någon av mobilens funktioner</h2>
  <p>Genom att klicka på knappen startas en timer mellan 3-6 sekunder som ska klickas på så fort som möjligt</p>
  <button @click="start" :disabled="isStarted">Starta timer</button>
  <button @click="loadElements" :disabled="isStarted">Ladda element</button>
  <ul v-if="fillers.length">
    <!-- <li v-for="filler in fillers" :key="filler.id"></li> -->
    <Filler v-for="filler in fillers" :key="filler.id" :joke="filler.joke"></Filler>
  </ul>
  <Clicker v-if="isStarted" :delay="delay" @reactionTime="result"></Clicker>
  <Result v-if="showResult" :time="time"></Result>
</template>

<script>
import Clicker from './components/Clicker.vue'
import Result from './components/Result.vue'
import Filler from './components/Filler.vue'
export default {
  name: 'App',
  components: { Clicker, Result, Filler },
  data(){
    return {
      isStarted: false,
      delay: null,
      time: null,
      showResult: false,
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
      .then(json => {
        this.fillers = json.value;
        })
      .catch(err => console.log('Error: ' + err.message))
    }
  },
  mounted() {

  }
}

</script>

<style>
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
