<template>
  <div class="container">
      <!-- <h1>This is a search page</h1> -->
    <div class="row">
        <div class="col-md-3" v-for="result in results" :key="result.idCategory" style="text-align: center;">
          <router-link :to="{ name: 'FilterKategori', params: { name: result.strCategory } }">
            <div class="card" style="width: 15rem; height: 90%;">
              <img class="card-img-top" :src="result.strCategoryThumb">
              <div class="card-body">
                <h5 class="card-title">{{result.strCategory}}</h5>
              </div>
            </div>
          </router-link>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Foods',
  data () {
    return {
      results: []
    }
  },
  mounted () {
    axios.get('https://www.themealdb.com/api/json/v1/1/categories.php').then(response => {
      console.log(response.data.categories)
      this.results = response.data.categories
    })
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
