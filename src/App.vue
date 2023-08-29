<script>

import { onMounted, ref } from 'vue';
import axios from 'axios';

export default {

  setup(){
    const endpoint = 'https://api-ssl.bitly.com/v4/shorten';
    const token = '71c9a899ed0dc44a8876f6833cbeffb7847f7f31';
    let guid = '';
    const url = ref('');
    const shortened_url = ref('');

    function shorten(){
      //  shortened_url.value = 
       axios.post(endpoint, {
          "group_guid": guid,
          "domain": "bit.ly",
          "long_url": url.value
        },
        {
        headers: {
            "Authorization": `Bearer ${token}`
          }
        }).then((res) => {
          // console.log(res.data)
          shortened_url.value = res.data.link;
        })
        .catch((error) => {
          console.error(error)
        });

        console.log(shortened_url);
    }

    onMounted(() => {
      axios.get('https://api-ssl.bitly.com/v4/groups',
        {
          headers: {
              "Authorization": `Bearer ${token}`
            }
        }).then((res) => {
          // console.log(res.data.groups[0].guid)
          guid = res.data.groups[0].guid;
        })
        .catch((error) => {
          console.error(error)
        })
    })

    return {
      url,
      shorten,
      shortened_url
    }
  }


}

</script>

<template>

  <input v-model="url">
  <button @click="shorten">Shorten</button>
  <div v-if="shortened_url">
    {{ shortened_url }}
  </div>

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
