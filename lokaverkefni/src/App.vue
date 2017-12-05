<template>
  <div id="app">
      <h1 id="AddYourTask">Add Your Task</h1>
      <input id="taskInput" class="text" type="text" v-model='task' v-on:keyup.enter='AddTask'>
      <button id="AddTaskButton" @click='AddTask'>Add Task</button>
    <div id="Tasks" v-for='task in tasks'>
      <ul>
        <li>
          <input id="checkbox" type="checkbox" @click='taskStatus(task.id)' :checked="(task.completed)">
          <label for="checkbox" class="text">{{ task.title }}</label>
        </li>
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
    };
  },
  mounted(){
    var self = this;
    axios.get('http://fjolbraut.org/api/tasks', {
        params: {
          api_token: 'jb5ZdxkzaL8dNs5VVyM1mu2YQCp9p3DIFxU7qcap32KLrqr5spVXGFA20K2e'}
        })
      .then(function(response) {
        self.tasks = response.data;
        console.log(response)
      })
      .catch(function(error) {
        console.log(error);
      });
    
  },
  methods: {
    AddTask: function(){
      axios.post('http://fjolbraut.org/api/tasks?api_token=jb5ZdxkzaL8dNs5VVyM1mu2YQCp9p3DIFxU7qcap32KLrqr5spVXGFA20K2e', {
            title: this.task
         })
         .then(function(response) {
          location.reload();
         })
         .catch(function(error) {
            console.log(error);
         });
    },
    taskStatus(id){
    
      axios.post('http://fjolbraut.org/api/tasks/' + id + '/status?api_token=jb5ZdxkzaL8dNs5VVyM1mu2YQCp9p3DIFxU7qcap32KLrqr5spVXGFA20K2e')
      .then(function(response) {
        location.reload();
      })
      .catch(function(error) {
        console.log(error);
      });
    }
  }
 }
</script>

<style >
body{
  background-color: #fcfcfc;
  padding-top: 50px;
  font-family: 'Courier New', sans-serif;
}

.text{
  color: #727272;
}

#app{
  text-align: center;
}

#AddYourTask{
  padding-bottom: 40px;
  font-size: 60px;
  color: #9b9b9b;
}

button{
  height: 50px;
  width: 150px;
  font-size: 20px;
  color: #ffffff;
  border: solid #000000 1px;
  border-radius: 2em;
  background-color: #000000;
}

#taskInput{
  height: 50px;
  width: 13.5em;
  margin-right: 80px;
  font-size: 25px;
  border: solid grey 1px;
  border-radius: 3px;
  background-color: #fcfcfc;
}

ul{
  list-style-type: none;
  background-color: #e8e8e8;
  border: solid #a5a5a5 1px;
  border-bottom: solid #e0e0e0 2px;
  height: 40px;
  font-size: 20px;
  padding-top: 16px;
  
}

#checkbox{
  float: left;
  height: 15px;
  width: 15px;
}

label{
  margin-right: 40px;
}

#Tasks{
  width: 640px;
  margin: auto;
}

input[type=checkbox]:checked + label.text{
  text-decoration: line-through;
}
</style>