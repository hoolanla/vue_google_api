<template>
  <div id="app" class="container">
    <p v-if="loading">Loading...</p>
    <div v-else>
      <h3 class="heading">Restaurant List</h3>
      <table class="table table-bordered">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Location</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="d in all_data" v-bind:key="d">
            <td>{{ d.id }}</td>
            <td>{{ d.name}}</td>
            <td>{{ d.vicinity }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'app',
  data () {
    return {
      loading: false,
      all_data: null
    }
  },
  mounted () {
    this.loading = true;
    axios
      .get('https://localhost:44365/api/GoogleMap')
      .then(response => (this.all_data = response.data.data))
      .catch(error => console.log(error))
      .finally(() => this.loading = false)
  }
}
</script>

<style>
#app {
  text-align: center;
  margin-top: 50px;
}
.heading {
  margin-bottom: 30px;
}
</style>