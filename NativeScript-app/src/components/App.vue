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
        showCountries: false,
        fillers: [
          {name:"Sweden", id:1}, 
          {name:"Norway", id:2}
          ]
      }
    },
  methods: {
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
