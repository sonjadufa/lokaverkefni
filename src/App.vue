<template>
  <div id="app">
      <h1>Verkefnalisti</h1>
    <input type="text" name="title" v-model="task" id="inputTag" placeholder="Hvað þarf að gera?" v-on:keyup.enter="taskInput">
    <button @click="taskInput">Bæta við</button>
      <div id="tasks" v-for="task in tasks">
        <ul class="list">
          <label><input type="checkbox" name="checkbox" id="checkbox"> {{ task.title }} </label>
          
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

    body{

      padding-left: 30%;
      padding-right: 30%;
    }

    ul{
      display: flex;
  /* Center everything inside .panel and li vertically */
      align-items: center;
  /* Distribute space evenly between the contents*/
      justify-content: space-between;
      list-style-type: none;
      padding: 10px;
      border-bottom: 1px solid #efefef;

    }

    #inputTag{
      margin-top: 5%; 
        padding-left: 10px;
      width: 88%;
      height: 20px;
    }

    button{
      height: 26px;
      border-radius: 5px;
    }

    button:hover{
      background-color: pink;
    }

    h1{
      text-align: center;
      font-family: georgia;
      text-decoration: underline;

    }


</style>
