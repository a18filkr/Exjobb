<template>
    <Page>
        <ActionBar>
            <Label text="List Test"></Label>
        </ActionBar>
        <StackLayout orientation="vertical">
          <Button @tap="loadElements" :isEnabled="!isLoaded" text="Ladda list" />
          <Button @tap="deleteElements" :isEnabled="!isDeleted" text="Radera Lista" />
          <ListView for="country in countries" @itemTap="countryTap" height="90%">
            <v-template>
                    <Label :text="country.name" class="label-padding"/>
            </v-template>
          </ListView>
        </StackLayout>

    </Page>
</template>

<script>

  export default {
    data() {
      return {
        countries: [
          { name: "Swe", id: 1},
          { name: "Norway", id: 2}
        ],
        isLoaded: false,
        isDeleted: true
      };
    },
    methods: {
      loadElements() {
      fetch('https://restcountries.eu/rest/v2/all')
        .then(resp => resp.json())
        .then(json => {
          this.countries = json
          this.showCountries = true
          })
        .catch(err => console.log('Error: ' + err.message));
        this.isLoaded = true;
        this.isDeleted = false;
      },
      deleteElements() {
        this.countries.splice(0, this.countries.length)
        this.isLoaded = false;
        this.isDeleted = true;
      },
      countryTap(e) {
        console.log(this.countries[e.index].name)
        console.log(this.countries[e.index].flag)
      }
    }
  };
</script>

<style scoped>

.label-padding {
  padding: 25px;
}

</style>
