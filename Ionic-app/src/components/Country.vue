<template>
  <ion-col size="4"></ion-col>
  <ion-col size="4">
    <ion-list mode="md">
      <ion-item button=true>
        <ion-label>{{ name }}</ion-label>
      </ion-item>
    </ion-list>
  </ion-col>
  <ion-col size="4"></ion-col>
</template>

<script>
import { IonCol, IonList, IonItem, IonLabel } from '@ionic/vue';

export default {
  components: { IonCol, IonList, IonItem, IonLabel },
  props: ['name']
}
</script>

<style scoped>
  li {
    text-decoration: none;
    list-style: none;
    background: #2c3e50;
    color: #e65a33;
    padding: 20px;
    max-width: 400px;
    margin: 5px auto;
    border-radius: 5px;
  }
</style>