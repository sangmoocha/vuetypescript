<template>
  <layout-welcome v-if="isAuth" />
  <layout-sign v-else />
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import LayoutWelcome from '@/components/layout/Welcome.vue';
import LayoutSign from '@/components/layout/Sign.vue';

@Component({
  components: {
    LayoutWelcome,
    LayoutSign
  }
})
export default class App extends Vue {
  isAuth = false;
}
</script>

<style scoped></style>
