<template>
  <div class="container">
    <ul>
      <li v-for="(item, index) in data.contents" :key="index">
        <nuxt-link :to="{ name: 'id', params: { id: item.id } }">
          {{ item.title }}
        </nuxt-link>
      </li>
    </ul>
    <p>
      <use-api-link />
    </p>
  </div>
</template>

<script>
import axios from 'axios'
import UseApiLink from '../components/UseApiLink.vue'
export default {
  components: { UseApiLink },
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
