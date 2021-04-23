<template>
    <Page>
        <ActionBar title="NativeScript Pilot-App"/>
        <!-- <StackLayout>
            <Label class="message" :text="msg2" height="auto" textWrap="true"/>
            <Label class="message" :text="msg" height="auto" textWrap="true"/>
            <Button @tap="start" :isEnabled="!isStarted" text="Starta timer" />
            <Button @tap="loadElements" :isEnabled="!isStarted" text="Ladda element" />
            <Clicker v-if="isStarted" :delay="delay" @reactionTime="result"></Clicker>
            <Result v-if="showResult" :time="time"></Result>
            <ScrollView height="60%">
              <StackLayout>
                <Filler v-for="filler in fillers" :key="filler.id" :name="filler.name"></Filler>
              </StackLayout>
            </ScrollView>
        </StackLayout> -->

        <TabView androidTabsPosition="bottom">
        <TabViewItem title="List">
            <Frame id="items">
                <Items/>
            </Frame>
        </TabViewItem>

        <TabViewItem title="Camera">
            <Frame id="browse">
                <Browse/>
            </Frame>
        </TabViewItem>

        <TabViewItem title="Tab3">
            <Frame id="search">
                <Search/>
            </Frame>
        </TabViewItem>
    </TabView>

    </Page>
</template>

<script >
  import Clicker from './Clicker.vue'
  import Result from './Result.vue'
  import Filler from './Filler.vue'
  import Items from "./Items.vue";
  import Browse from "./Browse.vue";
  import Search from "./Search.vue";

  export default {
    name: 'App',
    components: { Clicker, Result, Filler, Items, Browse, Search },
    data(){
      return {
        isStarted: false,
        delay: null,
        time: null,
        showResult: false,
        showCountries: false,
        fillers: [
          {name:"Sweden", id:1}, 
          {name:"Norway", id:2}
          ],
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
      fetch('https://restcountries.eu/rest/v2/all')
        .then(resp => resp.json())
        .then(json => {
          this.fillers = json
          this.showCountries = true
          })
        .catch(err => console.log('Error: ' + err.message))
    },
    onCountryTap(country) {
      console.log(country.index)
      console.log(country.item)
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
