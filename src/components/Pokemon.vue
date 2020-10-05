<template>
  <div>
		<h1>{{ number }} {{ name | upperFirstLetter }}</h1>
		<small>{{ url }}</small>
	</div>
</template>

<script>
	import axios from 'axios';

	export default {
		created: function() {
			axios.get(this.url)
				.then((response) => {
					this.pokemon.type = response.data.types[0].type.name;
					this.pokemon.imgFront = response.data.sprites.front_default;
					this.pokemon.imgBack = response.data.sprites.back_default;

					console.log(this.pokemon);
				})
		},
		data() {
			return {
				pokemon: {

				}
			}
		},
		props: {
			name: String,
			url: String,
			number: Number,
		},
		filters: {
			upperFirstLetter: function(value) {
				return value[0].toUpperCase() + value.slice(1);
			}
		}
	}
</script>

<style>

</style>