<template>
  <div>
    <form @submit.prevent="register">
      <label for="name">
        Name:
      </label>
      <input v-model="name" type="text" name="name" value>

      <label for="email">
        Email:
      </label>
      <input
        v-model="email"
        type="text"
        name="email"
        value
        autocomplete="username"
      >

      <label for="password">
        Password:
      </label>
      <input
        v-model="password"
        type="password"
        name="password"
        value
        autocomplete="current-password"
      >

      <button type="submit" name="button">
        Register
      </button>
      <ul>
        <li v-for="(error, index) in errors" :key="index">
          <p>{{ error }}</p>
        </li>
      </ul>
      <router-link to="/login">
        Already have an account? Login
      </router-link>
    </form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        password: '',
        errors: null
      }
    },
    methods: {
      register() {
        this.$store.dispatch('register', {
          name: this.name,
          email: this.email,
          password: this.password,
        }).then( () => {
          this.$router.push({name: 'dashboard'});
        })
          .catch(err => {
            console.log(err.message);
            this.errors = err.response.data.errors
          })
      }
    }
  }
</script>

<style scoped>

</style>
