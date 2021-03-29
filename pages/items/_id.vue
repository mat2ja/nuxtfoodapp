<template>
	<div>
		<pre>{{ currentItem }}</pre>
	</div>
</template>

<script>
import { mapState } from 'vuex';

export default {
	data() {
		return {
			id: this.$route.params.id,
		};
	},
	computed: {
		...mapState(['fooddata']),
		currentItem() {
			let result;

			for (let rest of this.fooddata) {
				result = rest.menu.find((meal) => meal.id === this.id);
				if (result) break;
			}

			return result;
		},
	},
};
</script>
