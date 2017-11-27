<template>
  <div id="app">
  <h2>{{  }}</h2>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  data () {
    return {
      tasks: []
    }
  },

  mounted() {
    var self = this;
    axios.get('http://fjolbraut.org/api/tasks', {
      params: {
        api_token: 'G0h6P9g4NcH94VsGg8CHTeqfJYH1YikmZwXHbJHXmBuogVaNxQdT6ZKlyOwc'
          }
        })
        
        .then(function(response) {
          self.tasks = response.data
          console.log(response);
          })
     .catch(function(error) {
          console.log(error);
        });
  }
}
</script>

<style lang="scss">

</style>
