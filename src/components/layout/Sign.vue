<template>
  <v-card>
    <v-btn @click="test">tset</v-btn>
  </v-card>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class LayoutSign extends Vue {
  test() {
    console.log(this.$firebase);
  }
}
</script>

<style scoped></style>
