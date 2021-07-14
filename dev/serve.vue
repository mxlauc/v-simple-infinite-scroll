<template>
  <div id="app">
    <home-component></home-component>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import HomeComponent from './HomeComponent.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    HomeComponent
  }
});
</script>
