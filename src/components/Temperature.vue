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
	import imageDespejado from './assets_components/despejado.svg'
	import imagenNublado from './assets_components/nublado.svg'
	import imagenLLuvia from './assets_components/lluvia.svg'


	const stringConverterToInt = string => parseInt(string);

	//traduzco lo que significa cada estado del clima
	const stateTranslated = string => {
		if (string == "Clear") {
			return "Despejado"
		}else if (string == "Clouds") {
			return "Nublado"
		}else if (string == "Rain") {
			return "Lluvia"
		}
	}

	//esta funcion devuelve la imagen a mostrar
	const imageState = state => {
		if (state == 'Despejado') {
			return imageDespejado
		}else if (state == "Nublado") {
			return imagenNublado
		}else if (state == "Lluvia") {
			return imagenLLuvia
		}
	}

	export default{
		name: 'Temperature',
		data(){
			return{
				image: [],
				temperature: [],
				state: []
			}
		},
		mounted () {
			axios
				.get('http://fcc-weather-api.glitch.me/api/current?lat=-27.440808&lon=-59.009453')
				.then(respuesta => {
					this.temperature = stringConverterToInt(respuesta.data.main.temp);
					this.state = stateTranslated(respuesta.data.weather[0].main);
					this.imagen = imageState(this.state);
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