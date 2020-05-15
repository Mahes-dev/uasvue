<template>
  <div class="foods">
    <div class="row my-5">
        <div class="form-inline" style="width: 100%">
            <div class="form-group mx-sm-2 mb-2">
                <input type="text" class="form-control" placeholder="Seach meals by name..." v-model="query">
            </div>
            <button type="submit" class="btn btn-primary mb-2" @click="getResult(query)">Search</button>
        </div>
    </div>
    <div class="row">
        <div class="col-md-3" v-for="result in results" :key="result.idMeal" style="text-align: center;">
          <div class="card" style="width: 15rem; height: 90%;" @click="goToDetail(result.idMeal)">
            <img class="card-img-top" :src="result.strMealThumb">
            <div class="card-body">
              <h5 class="card-title">{{result.strMeal}}</h5>
             <span class="badge badge-pill badge-primary">{{result.strCategory}}</span>
            </div>
          </div>`
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
      msg: 'Search',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult (query) {
      axios.get('https://www.themealdb.com/api/json/v1/1/search.php?s=' + query).then(response => {
        console.log(response.data.meals)
        this.results = response.data.meals
      })
    },
    goToDetail (mealId) {
      this.$router.push({ name: 'Detail', params: { mId: mealId } })
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
