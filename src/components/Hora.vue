<template>
	<p id="hora_cliente" class="text-muted">{{ hora }}</p>
</template>

<script>
	const horaCliente = () => {
		var date = new Date;
		return date.getHours()+":"+date.getMinutes()
	}

	export default{
		name:'Hora',
		data(){
			return{
				hora: horaCliente()
			}
		}
	}
</script>

<style>
	#hora_cliente{
		text-align: center;
		font-size: 30px;
		margin-top: 5%;
	}
</style>