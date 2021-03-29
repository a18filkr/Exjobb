<template>
    <Page>
        <ActionBar title="NativeScript Pilot-App"/>
        <StackLayout>
            <Label class="message" :text="msg2" height="auto" textWrap="true"/>
            <Label class="message" :text="msg" height="auto" textWrap="true"/>
            <Button @tap="start" :isEnabled="!isStarted" text="Starta timer" />
            <Button @tap="loadElements" :isEnabled="!isStarted" text="Ladda element" />
            <Clicker v-if="isStarted" :delay="delay" @reactionTime="result"></Clicker>
            <Result v-if="showResult" :time="time"></Result>
            <Filler v-for="filler in fillers" :key="filler.id" :joke="filler.joke"></Filler>
        </StackLayout>
    </Page>
</template>

<script >
  import Clicker from './Clicker.vue'
  import Result from './Result.vue'
  import Filler from './Filler.vue'
  export default {
    name: 'App',
    components: { Clicker, Result, Filler },
    data(){
      return {
        isStarted: false,
        delay: null,
        time: null,
        showResult: false,
        fillers: [{ id: 72, joke: "How much wood would a woodchuck chuck if a woodchuck could Chuck Norris? All of it." }],
        msg: 'Genom att klicka på knappen startas en timer mellan 3-6 sekunder som ska klickas på så fort som möjligt',
        msg2: 'Liten testapp för att se vad som skiljer i NativeScript och Ionic utan att använda någon av mobilens funktioner'
      }
    },
  methods: {
    start() {
      this.delay = Math.floor(3000 + Math.random() * 3000)
      this.isStarted = true
      this.showResult = false;
      console.log(this.isStarted, this.delay, this.showResult);
    },
    result(time) {
      this.time = time
      this.isStarted = false
      this.showResult = true
      console.log("This is the time:", this.time)
    },
    loadElements() {
      fetch('http://api.icndb.com/jokes/random/25')
        .then(resp => resp.json())
        .then(json => this.fillers = json)
        .catch(err => console.log('Error: ' + err.message))
    }
  }
}

</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 16;
        color: #333333;
        margin: 15 0;
        padding: 5;
    }
</style>
