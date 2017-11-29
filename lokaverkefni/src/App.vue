<template>
  <div id="app">
    	<input type="text" v-model='task'>
    	<button @click='taskInput'>bæta við</button>
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
  	taskInput: function(){

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

<style lang="scss">
</style>