<template>
 <div class="login-form">
   <div v-if="error">
    <b-alert show dismissible variant="danger">
      <b>{{error}}</b>
    </b-alert>
  </div>
    <form @submit.prevent="submit">
        <h2 class="text-center">Log in</h2>
        <div class="form-group">
            <input type="text" class="form-control" placeholder="Email" required="required" name="email" v-model="form.email">
        </div>
        <div class="form-group">
            <input type="password" class="form-control" placeholder="Password" required="required" name="password" v-model="form.password">
        </div>
        <div class="form-group">
            <button type="submit" class="btn btn-primary btn-block">Log in</button>
        </div>
    </form>
    <p class="text-center"><router-link to="/register">Create an Account</router-link></p>
</div>
</template>

<script>
import firebase from 'firebase'

export default {
  data () {
    return {
      form: {
        email: '',
        password: ''
      },
      error: null
    }
  },
  methods: {
    submit () {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.form.email, this.form.password)
        .then(data => {
          console.log(data)
          this.$router.replace({ name: 'Home' })
        })
        .catch(err => {
          this.error = err.message
        })
    }
  }
}
</script>

<style>
  .login-form {
    width: 340px;
    margin: 50px auto;
  }
    .login-form form {
    margin-bottom: 15px;
    background: #f7f7f7;
    box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.3);
    padding: 30px;
  }
    .login-form h2 {
    margin: 0 0 15px;
  }
    .form-control, .btn {
    min-height: 38px;
    border-radius: 2px;
  }
    .btn {
    font-size: 15px;
    font-weight: bold;
  }
</style>
