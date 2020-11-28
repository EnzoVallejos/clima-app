<template>
	<div class="row">
		<div class="col-4 ml-5 mt-4">
			<img v-bind:src="imagen" height="150" weight="150">
		</div>
		
		<div class="col-4" id="container_temp_state">
			<p id="temperature">{{ temperature }}°</p>
			<p id="state" class="text-muted">{{ state }}</p>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	import image_despejado from './assets_components/despejado.svg'

	//esta funcion devuelve la imagen a mostrar
	const image_state = state => {
		if (state == 'Despejado') {
			return image_despejado
		}
	}

	const string_converter_to_int = string => parseInt(string);

	//traduzco lo que significa cada estado del clima
	const state_translated = string => {
		if (string == "Clear") {
			return "Despejado"
		}
	}

	export default{
		name: 'Temperature',
		data(){
			return{
				image_state: "",
				temperature: "",
				state: ""
			}
		},
		mounted () {
			axios
				.get('http://fcc-weather-api.glitch.me/api/current?lat=-27.440808&lon=-59.009453')
				.then(respuesta => {
					this.temperature = string_converter_to_int(respuesta.data.main.temp);
					this.state = state_translated(respuesta.data.weather[0].main);
					this.imagen = image_state(this.state);
				})
		}
	}
</script>

<style>
	#container_temp_state{
		margin-top: 12%;
		margin-left: 13%;
	}

	#temperature, state{
		margin: 0;
	}

	#temperature{
		font-weight: bold;
		font-size: 50px;
	}

	#state{
		margin-top: -6%;
		margin-left: -6%;
	}
</style>