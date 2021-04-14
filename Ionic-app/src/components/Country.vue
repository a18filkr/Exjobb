<template>
  <ion-item button=true>
    <ion-label>{{ name }}</ion-label>
    <!-- <ion-label>{{ icon }}</ion-label> -->
    <ion-thumbnail slot="end">
      <ion-img :src="icon" alt="" />
    </ion-thumbnail>
  </ion-item>
</template>

<script>
import { IonItem, IonLabel, IonThumbnail, IonImg } from '@ionic/vue';

export default {
  components: { IonItem, IonLabel, IonThumbnail, IonImg },
  props: ['name', 'icon']
}
</script>

<style scoped>
</style>