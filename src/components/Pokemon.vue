<template>
  <div>
		<h1>{{ number }} {{ name | upperFirstLetter }}</h1>
		<small>{{ url }}</small>
	</div>
</template>

<script>
	export default {
		props: {
			number: Number,
			name: String,
			url: String
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