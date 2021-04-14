<template>
  <ion-item button=true>
    <ion-label>{{ name }}</ion-label>
  </ion-item>
</template>

<script>
import { IonItem, IonLabel } from '@ionic/vue';

export default {
  components: { IonItem, IonLabel },
  props: ['name']
}
</script>

<style scoped>
</style>