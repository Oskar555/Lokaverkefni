<template>
  <div id="app">
  		<h1 id="AddYourTask">Add Your Task</h1>
    	<input id="taskInput" type="text" v-model='task' v-on:keyup.enter='AddTask'>
    	<button id="AddTaskButton" @click='AddTask'>Add Task</button>
    <div id="Tasks" v-for='task in tasks'>
    	<ul>
    		<li>
    			<label><input id="checkbox" type="checkbox" @click='taskStatus'>{{ task.title }}</label>
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
  			
        })
        .catch(function(error) {
            console.log(error);
         });
  	}
  },
  computed: {
  	
  	}
  }
</script>

<style >

body{
	padding-top: 70px;
	font-family: Optima, Segoe, "Segoe UI", Candara, Calibri, Arial, sans-serif;
}

#app{
	text-align: center;
}

#AddYourTask{
	padding-bottom: 50px;
	font-size: 60px;
}

button{
	height: 50px;
	width: 150px;
	font-size: 20px;
}

#taskInput{
	height: 50px;
	width: 30em;
	margin-right: 100px; 
}

ul{
	list-style-type: none;
	background-color: #ddffe2;
	

}

#Tasks{
	padding-right: 621px;
	padding-left: 621px;

}

</style>