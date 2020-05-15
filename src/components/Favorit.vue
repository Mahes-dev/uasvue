<template>
  <div class="home" >
      <!-- <h1>This is a search page</h1> -->
    <div class="row my-5">
        <center>
        <div class="form-inline" style="width: 100%;">
        </div>
        </center>
    </div>
    <div class="row" v-if="user.loggedIn">
        <div class="col-md-3" v-for="result in fav" :key="result.id" style="text-align: center;">
          <router-link :to="{ name: 'Detail', params: { id: result.id } }">
          <div class="card" style="width: 15rem; height: 90%;">
            <img class="card-img-top" :src="result.picture">
            <div class="card-body">
              <h5 class="card-title">{{result.name}}</h5>
             <span class="badge badge-pill badge-primary">{{result.category}}</span>
            </div>
          </div>
          </router-link>`
        </div>
    </div>
    <b-container v-else  >
      <div>
        <h2>Silahkan login terlebih dahulu untuk menggunakan halaman ini</h2>
           <img  src="../assets/login.jpg" width="400px" height="400px">
      </div>
      <br/>
      <br/>
      <br/>
    </b-container>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import firebase from 'firebase'
const STORAGE_KEY = 'DATAFAVORIT'
export default {
  name: 'Home',
  data () {
    return {
      msg: 'Search',
      query: '',
      results: '',
      fav: []

    }
  },
  async created () {
    this.fav = JSON.parse(localStorage.getItem(STORAGE_KEY) || [])
    console.log(this.fav)
  },
  computed: {
    ...mapGetters({
      // map `this.user` to `this.$store.getters.user`
      user: 'user'
    })
  },
  methods: {
    signOut () {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$router.replace({
            name: 'Login'
          })
        })
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
