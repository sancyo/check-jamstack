<template>
  <div class="container">
    <h2>ここではAPIをたたいてコンテンツを表示します</h2>
    <ul v-if="!isOpen">
      <li v-for="(item, index) in data.contents" :key="index">
        <nuxt-link
          :to="{ name: 'use-api-id', params: { id: item.id } }"
          event=""
          @click.native="clickOpen(item.id)"
        >
          {{ item.title }}
        </nuxt-link>
      </li>
    </ul>
    <button v-if="isOpen" @click="clickClose()">閉じる</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      isOpen: false,
      data: '',
      getData: '',
    }
  },
  async created() {
    const { data } = await axios.get(
      `https://designdock02.microcms.io/api/v1/posts`,
      {
        headers: { 'X-API-KEY': process.env.API_KEY },
      }
    )
    this.data = data
  },
  methods: {
    clickOpen(id) {
      this.isOpen = true
      history.pushState({}, 'showPost', `/use-api/${id}`)
      this.getContent(id)
    },
    clickClose() {
      this.isOpen = false
      history.back()
      this.getData = ''
    },
    async getContent(id) {
      const { data } = await axios.get(
        `https://designdock02.microcms.io/api/v1/posts/${id}`,
        {
          headers: { 'X-API-KEY': 'd8d93431-5281-4b77-8f54-33e795130bca' },
        }
      )
      this.getData = data
    },
  },
}
</script>
