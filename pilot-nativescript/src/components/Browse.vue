<template lang="html">
    <Page class="page">
        <ActionBar class="action-bar">
            <Label class="action-bar-title" text="Photo test"></Label>
        </ActionBar>
        
        <StackLayout class="page__content">
        <AbsoluteLayout>
          <Label 
            text="Take Picture"
            textWrap="true"
            textAlignment="center"
            left="50%"
            top="50%"
            width="75"
            height="75"
            backgroundColor="#43b883"
            borderRadius="50"
            @tap="takePicture" 
          />
        </AbsoluteLayout>
            <ScrollView class="picture-gallery" orientation="vertical">
              <StackLayout>
                <Image v-for="image in arrayPictures" :src="image" class="gallery-item" stretch="aspectFit" />
              </StackLayout>
            </ScrollView>
            
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
