<template>


	<div class="container">
		<div>
			<h2>Upload your file !</h2>
		

			<v-btn color="success" @click="$refs.inputUpload.click()">Uplad your script</v-btn>
			<input v-show="false" ref="inputUpload" type="file" @change="handleFileUpload( $event )" >
			<br>
			<br>
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
		  Be careful ! 1 monero = 150 $ approximately !
        
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
				file: '',
				ntime: '',
				reward: ''
			}
		},
		
		methods: {
			handleFileUpload( event ){
				this.file = event.target.files[0];
			},
			
			submitFile(){
				let formData = new FormData();
				formData.append('files', this.file);
				axios.post( 'https://api.masternetwork.dev/upload/python?uid='+this.$fire.auth.W+'&ntime='+this.ntime+'&reward='+this.reward,
					formData,
					{
						headers: {
								'Content-Type': 'multipart/form-data'
						}
					}
				).then(function(){
					console.log('SUCCESS!!');
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