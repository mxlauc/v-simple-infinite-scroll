<script>
import { defineComponent } from 'vue';
import VSimpleInfiniteScroll from '@/v-simple-infinite-scroll.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    VSimpleInfiniteScroll
  }
});
</script>

<template>
  <div id="app">
    <v-simple-infinite-scroll>
      hola gg
    </v-simple-infinite-scroll>
  </div>
</template>
