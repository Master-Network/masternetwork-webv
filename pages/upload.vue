<template>


	<div class="container">
		<div>
			<h2>Upload your file !</h2>
		

			<v-btn color="success" @click="$refs.inputUpload.click()">Uplad your script</v-btn>
			<input v-show="false" ref="inputUpload" type="file" webkitdirectory mozdirectory @change="handleFileUpload( $event )">
	<br><br><br>
			   <label>Name of the script</label>
			<input

            type="string"
            v-model="name"
            class="form-control"
            placeholder="my script"
          ><br><br><br>
		  <label>Repeat</label>
          <input

            type="number"
            v-model="ntime"
            class="form-control"
            placeholder="280"
          >
		  
        
			<br>
				<br>
			<br>
			   <label>Reward in monero</label>
          <input
            type="number"
            v-model="reward"
            class="form-control"
            placeholder="0.00001" 
          > 
		  Be careful ! 1 monero = 180 $ approximately !
        
			<br>
			<button v-on:click="submitFile()"><u>Submit</u></button>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	
	export default {
		data(){
			return {
				files: '',
				name : '',
				ntime: '',
				reward: ''
			}
		},
		
		methods: {
			handleFileUpload( event ){
				this.files = event.target.files
			},
			
			submitFile(){
				let formData = new FormData();
				
				for( var i = 0; i < this.files.length; i++ ){
					let file = this.files[i];
				
					formData.append('files', file);
					console.log('files=', file)
				}
				console.log( 'https://api.masternetwork.dev/upload/files/?uid='+this.$fire.auth.W+'&name='+this.name+'&timetodo='+this.ntime+'&reward='+this.reward,
					formData,
					{
						headers: {
								'Content-Type': 'multipart/form-data'
						}
					})
				axios.post( 'https://api.masternetwork.dev/upload/files/?uid='+this.$fire.auth.W+'&name='+this.name+'&timetodo='+this.ntime+'&reward='+this.reward,
					formData,
					{
						headers: {
								'Content-Type': 'multipart/form-data'
						}
					}
				).then(function(){
					console.log('SUCCESS!!');
					window.location.reload(true)
				})
				.catch(function(){
					console.log('FAILURE!!');
				});
			}
		}
	}
</script>
<style>
.form-control {
	color: white
}
</style>