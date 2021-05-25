<template>
    <Page>
        <ActionBar title="NativeScript Pilot-App"/>

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
  import Filler from './Filler.vue'
  import Items from "./Items.vue";
  import Browse from "./Browse.vue";
  import Search from "./Search.vue";

  export default {
    name: 'App',
    components: { Filler, Items, Browse, Search },
    data(){
      return {
        delay: null,
        time: null,
        fillers: [
          {name:"Sweden", id:1}, 
          {name:"Norway", id:2}
          ]
      }
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
      fetch("../assets/json/covid-vaccin.json")
      .then(resp => resp.json())
      .then(json => this.listobjects = json.records)
      .catch(err => console.log('Error: ' + err.message))
      this.isLoaded = true
      this.isDeleted = false
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
