<template>
	<div class="row">
		<div class="col-4">
			<img v-bind:src="image.icon" height="200" weight="200">
		</div>
		
		<div class="col-4">
		</div>
		
		<div class="col-4">
			<p>{{ temperature.temp }}</p>
			<p>{{ state }}</p>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	export default{
		name: 'Temperature',
		data(){
			return{
				image: "",
				temperature: "",
				state: ""
			}
		},
		mounted () {
			axios
				.get('http://fcc-weather-api.glitch.me/api/current?lat=-27.440808&lon=-59.009453')
				.then(respuesta => {
					this.image = respuesta.data.weather[0];
					this.temperature = respuesta.data.main;
					this.state = respuesta.data.weather[0].main;
				})
		}
	}
</script>