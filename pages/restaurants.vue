<template>
	<main class="container restaurant">
		<div class="restaurantheading">
			<h1>Restaurants</h1>

			<AppSelect @change="selectedRestaurant = $event" />
			<!-- awesome debugging trick! -->
			<pre>{{ $data }}</pre>
		</div>

		<AppRestaurantInfo />
	</main>
</template>

<script>
import AppRestaurantInfo from '@/components/AppRestaurantInfo.vue';
import AppSelect from '@/components/AppSelect.vue';

export default {
	components: {
		AppRestaurantInfo,
		AppSelect,
	},
	data() {
		return {
			selectedRestaurant: '',
		};
	},
};
</script>