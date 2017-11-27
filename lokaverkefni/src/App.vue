<template>
  <div id="app">
    <div id="tasks" v-for='task in tasks'>
    	<h1>{{ tasks.data }}</h1>
    </div>
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
  mounted(){
  	var self = this;

  	axios.get('http://fjolbraut.org/api/tasks', {
        params: {
        	api_token: 'jb5ZdxkzaL8dNs5VVyM1mu2YQCp9p3DIFxU7qcap32KLrqr5spVXGFA20K2e'
            }
        })
  	.then(function(response) {
  		self.tasks = response.data.results;
  		console.log(response)
  	})
  	.catch(function(error) {
  		console.log(error);
  	});
  },
  computed: {
  	
  }
}
</script>

<style lang="scss">

</style>
