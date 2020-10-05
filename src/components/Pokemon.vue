<template>
  <div id="pokemon">
		<div class="card">
			<div class="card-image">
				<figure>
					<img :src="pokemon.imgFront" alt="Placeholder image">
				</figure>
			</div>
			<div class="card-content">
				<div class="media">
					<div class="media-content">
						<p class="title is-4">{{ number }} {{ name | upperFirstLetter }}</p>
						<p class="subtitle is-6">{{ pokemon.type }}</p>
					</div>
				</div>

				<div class="content">
				</div>
			</div>
		</div>
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
					type: '',
					imgFront: '',
					imgBack: ''
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
	#pokemon {
		margin-bottom: 2%;
	}
</style>