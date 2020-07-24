<template>
  <section class="container">
    <h1>Authorization form</h1>
    <v-form>
      <v-container>
        <v-row>
          <v-col
            cols="12"
            md="4"
          >
            <v-text-field
              v-model="form.login"
              :append-icon = "'mdi-account'"
              label="Login"
            />
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="form.password"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show1 ? 'text' : 'password'"
              name="input"
              label="password"

              @click:append="show1 = !show1"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="12">
            <v-btn @click="submit">
              Login
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
  </section>
</template>

<script>
  export default {
    data () {
      return {
        form: {
          login: 'LOGIN',
          password: 'PASSWORD'
        },
        show1: false,

        password: '',
        rules: {
          required: value => !!value || 'Required.',
          min: v => v.length >= 8 || 'Min 8 characters',
          emailMatch: () => ('The email and password you entered don\'t match'),
        },
      }
    },
    methods: {
      async submit() {
        try {
          await this.$store.dispatch('auth/login', this.form)
          this.$router.push('/')
        } catch (e) {
          console.log(e)
        }
      }
    }
  }
</script>
