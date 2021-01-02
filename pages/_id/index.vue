<template>
  <div class="container">
    <h2>{{ data.title }}</h2>
    <p>{{ data.content }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://designdock02.microcms.io/api/v1/posts/${params.id}`,
      {
        headers: { 'X-API-KEY': process.env.API_KEY },
      }
    )
    console.log(params.id)
    return {
      data,
    }
  },
}
</script>
