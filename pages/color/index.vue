<template>
  <section class="container">
    <div>
      <span>color 一覧</span>
      <span>|</span>
      <span><nuxt-link to="/scheme">scheme</nuxt-link></span>
    </div>
    <div><img :src="data.image.named" /></div>

    <div><img :src="changes.image.named"/></div>
    <input type="button" value="change" @click="changeColor()"/>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData () {
    const hex = Math.floor(Math.random() * 16777215).toString(16)
    const { data } = await axios.get(`http://www.thecolorapi.com/scheme?hex=${hex}`)
    return { data }
  },
  data () {
    return {
      changes: {
        image: {
          named: null
        }
      }
    }
  },
  methods: {
    async changeColor () {
      const hex = Math.floor(Math.random() * 16777215).toString(16)
      const { data } = await axios.get(`http://www.thecolorapi.com/scheme?hex=${hex}`)
      this.changes = data
      return { data }
    }
  }
}
</script>

<style scoped>

</style>
