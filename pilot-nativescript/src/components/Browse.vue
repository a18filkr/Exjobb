<template lang="html">
    <Page class="page">
        <ActionBar class="action-bar">
            <Label class="action-bar-title" text="Photo test"></Label>
        </ActionBar>
        
        <StackLayout class="page__content">

            <ScrollView height="80%" class="picture-gallery" orientation="vertical">
              <StackLayout>
                <Image v-for="image in arrayPictures" :src="image" class="gallery-item" stretch="aspectFit" />
              </StackLayout>
            </ScrollView>
                  
          <Button 
            text="Take Photo"
            textWrap="true"
            width="80"
            height="80"
            margin="5"
            backgroundColor="#43b883"
            borderRadius="50"
            androidElevation="4"
            @tap="takePicture" 
          />
        
        </StackLayout>
    </Page>
</template>

<script>
const cameraModule = require("nativescript-camera");
  export default {
    computed: {},
    data() {
      return {
        arrayPictures: []
      };
    },
    methods: {
      takePicture() {
        let that = this;
        cameraModule.takePicture({
          width: 300,
          height: 300,
          keepAspectRatio: true,
          saveToGallery: false
        })
        .then (imageAsset => {
          that.arrayPictures.unshift(imageAsset)
        })
      }
    },
    mounted() {
      cameraModule.requestPermissions().then(
        success => {

        },
        failure => {

        }
      )
    }
  }
</script>

<style lang="scss" scoped>
.take-picture-icon {
  text-align: center;

  border-width: 1.2;
  border-color: black;
  color: white;
  font-size: 20;
  border-radius: 50%;
}

.picture-gallery {
  margin-top: 20;
}

.gallery-item {
  margin: 10;
}
</style>
