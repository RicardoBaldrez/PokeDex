<template>
  <div id="pokemon">
		<div class="card">
			<div class="card-image">
				<figure>
					<img :src="currentImg" alt="Placeholder image">
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
					<button class="button is-danger is-rounded is-small" @click="alterSprite">Trocar sprite</button>
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
					this.currentImg = this.pokemon.imgFront;
				})
		},
		data() {
			return {
				isFront: true,
				currentImg: '',
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
		},
		methods: {
			alterSprite: function() {
				if(this.isFront) {
					this.isFront = false;
					this.currentImg = this.pokemon.imgBack;
				} else {
					this.isFront = true;
					this.currentImg = this.pokemon.imgFront;
				}
			}
		}
	}
</script>

<style>
	#pokemon {
		margin-bottom: 2%;
	}
</style>