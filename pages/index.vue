<template>
  <section class="container">
    
    
    <p>name: {{ user.name }}</p>
    <p>email: {{ user.email }}</p>

    <v-avatar size="100">
      <img :src="user.image" alt="Pavel">
    </v-avatar>
  </section>
</template>

<script>

export default {
  middleware: 'auth',
  data () {
    return {
      user: {
        name: '',
        email: '',
        image: ''
      }
    }
  },
  async asyncData({ $axios }) {
    const user = await $axios.get('https://pvpavlov-frontend.github.io/mockData.json')

    return { user: user.data }
  }
}
</script>
