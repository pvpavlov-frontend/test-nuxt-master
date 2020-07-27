<template>

    <v-container>
      <v-row>
        <v-col cols="12">
          <v-avatar size="100">
            <img :src="user.image" alt="Pavel">
          </v-avatar>
        </v-col>
        <v-col cols="12">
          <p >name: {{ user.name }}</p>
          <p>email: {{ user.email }}</p>
        </v-col>
      </v-row>
    </v-container>
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
