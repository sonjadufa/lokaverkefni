<template>
  <div id="app">
    <input type="text" name="title" v-model="task">
    <button @click="taskInput">Bæta við</button>
      <div id="tasks" v-for="task in tasks">
        <ul>
          <label><input type="checkbox" name="checkbox" id="checkbox" @click="taskStatus"> {{ task.title }} </label>
          
        </ul>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  data () {
    return {
      tasks: [],
      task: ''
      
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
  },
  
  methods: {
    taskInput: function() {
      axios.post('http://fjolbraut.org/api/tasks?api_token=G0h6P9g4NcH94VsGg8CHTeqfJYH1YikmZwXHbJHXmBuogVaNxQdT6ZKlyOwc', {
            title: this.task
         })
         .then(function(response) {
          location.reload();

          
         })
         .catch(function(error) {
            console.log(error);
         });


      //this.tasks.push(this.task);
      //this.task = ''
    }, 

    taskStatus(id){
    

    axios.post('http://fjolbraut.org/api/tasks/' + id + '/status?api_token=G0h6P9g4NcH94VsGg8CHTeqfJYH1YikmZwXHbJHXmBuogVaNxQdT6ZKlyOwc')
        .then(function(response) {
            console.log(response);
        })
        .catch(function(error) {
            console.log(error);
         });
      }
  }
}
</script>

<style>

</style>
