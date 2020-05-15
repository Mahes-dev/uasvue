<template>
  <div class="search container">
  <Food />
  </div>
</template>

<script>
// @ is an alias to /src
import Food from '@/components/Home.vue'

export default {
  name: 'Search',
  components: {
    Food
  }
}
</script>
