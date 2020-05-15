<template>
 <div class="register-form">
  <div v-if="error">
    <b-alert show dismissible variant="danger">
      <b>{{error}}</b>
    </b-alert>
  </div>
    <form @submit.prevent="submit">
        <h2 class="text-center">Register</h2>
         <div class="form-group">
            <input type="text" class="form-control" placeholder="Name" required="required" v-model="form.name" name="name">
        </div>
        <div class="form-group">
            <input type="text" class="form-control" placeholder="Email" required="required" v-model="form.email" name="email">
        </div>
        <div class="form-group">
            <input type="password" class="form-control" placeholder="Password" required="required" v-model="form.password" name="password">
        </div>
        <div class="form-group">
            <button type="submit" class="btn btn-primary btn-block">Register</button>
        </div>
    </form>
    <p class="text-center" v-if="onRegisterPage"></p>
</div>
</template>

<script>
import firebase from 'firebase'

export default {
  data () {
    return {
      form: {
        name: '',
        email: '',
        password: ''
      },
      onRegisterPage: true,
      error: null
    }
  },
  methods: {
    submit () {
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.form.email, this.form.password)
        .then(data => {
          data.user
            .updateProfile({
              displayName: this.form.name
            })
            .then(() => {})
        })
      this.$router.replace({ name: 'Login' })
        .catch(err => {
          this.error = err.message
        })
    }
  }
}
</script>
<style>
  .register-form {
    width: 340px;
    margin: 50px auto;
  }
    .register-form form {
    margin-bottom: 15px;
    background: #f7f7f7;
    box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.3);
    padding: 30px;
  }
    .register-form h2 {
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
