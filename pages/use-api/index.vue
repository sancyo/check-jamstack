<template>
  <div class="container">
    <h2>ここではAPIをたたいてコンテンツを表示します</h2>
    <p>{{ data }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      data: '',
    }
  },
  async created() {
    const { data } = await axios.get(
      `https://designdock02.microcms.io/api/v1/posts`,
      {
        headers: { 'X-API-KEY': 'd8d93431-5281-4b77-8f54-33e795130bca' },
      }
    )
    console.log(data)
    this.data = data
    return {
      data,
    }
  },
}
</script>
