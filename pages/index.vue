<template>
  <div class="container">
    <ul>
      <li v-for="(item, index) in data.contents" :key="index">
        <nuxt-link :to="{ name: 'id', params: { id: item.id } }">
          {{ item.title }}
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  async asyncData() {
    const { data } = await axios.get(
      'https://designdock02.microcms.io/api/v1/posts',
      {
        headers: { 'X-API-KEY': process.env.API_KEY },
      }
    )
    console.log(data)
    return {
      data,
    }
  },
  mounted() {
    console.log(process.env.API_KEY)
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
