<script>

import { ref } from 'vue';

export default {

  setup(){

    const url = ref('asdasd');

    function shorten(){
      let shortened_url = url.value;
    }

    return {
      url,
    }
  }


}

</script>

<template>

  <p>test</p>

  <input v-model="url">
  <button @click="shorten">shorten</button>

</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
