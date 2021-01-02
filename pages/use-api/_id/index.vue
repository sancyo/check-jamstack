<template>
  <div class="container">
    <h2>このページコンテンツをnuxt generateで静的化したい</h2>
    {{ data }}
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
    return {
      data,
    }
  },
}
</script>
