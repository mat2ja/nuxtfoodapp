<template>
	<main class="container">
		<section
			class="image"
			:style="`background: url(/${currentItem.img}) no-repeat center center`"
		/>

		<section class="details">
			<h1>{{ currentItem.item }}</h1>
			<h3>Price: ${{ currentItem.price.toFixed(2) }}</h3>

			<div class="quantity">
				<input type="number" min="1" v-model="$v.count.$model" />
				<button class="primary" @click="addToCart">
					Add to cart
					<span v-if="!$v.count.$invalid">
						- ${{ combinedPrice }}</span
					>
				</button>
			</div>

			<fieldset v-if="currentItem.options">
				<legend>
					<h3>Options</h3>
				</legend>
				<div v-for="option in currentItem.options" :key="option">
					<input
						type="radio"
						name="option"
						:id="option"
						:value="option"
						v-model="$v.itemOptions.$model"
					/>
					<label :for="option">{{ option }}</label>
				</div>
			</fieldset>

			<fieldset v-if="currentItem.addOns">
				<legend>
					<h3>Add Ons</h3>
				</legend>
				<div v-for="addOn in currentItem.addOns" :key="addOn">
					<input
						type="checkbox"
						name="addOn"
						:id="addOn"
						:value="addOn"
						v-model="$v.itemAddons.$model"
					/>
					<label :for="addOn">{{ addOn }}</label>
				</div>
			</fieldset>

			<AppToast v-if="cartSubmitted">
				Order submitted!<br />
				Check out more
				<nuxt-link to="/restaurants">restaurants</nuxt-link>
			</AppToast>

			<AppToast v-if="errors">
				Please select options and
				<br />addons before continuing
			</AppToast>
		</section>
	</main>
</template>

<script>
import { mapState } from 'vuex';
import AppToast from '@/components/AppToast.vue';
import { required, minValue, numeric } from 'vuelidate/lib/validators';

export default {
	components: {
		AppToast,
	},
	data() {
		return {
			id: this.$route.params.id,
			count: 1,
			itemOptions: [],
			itemAddons: [],
			itemSizeAndCost: [],
			cartSubmitted: false,
			errors: false,
		};
	},
	validations: {
		itemOptions: {
			required,
		},
		itemAddons: {
			required,
		},
		count: {
			required,
			numeric,
			minValue: minValue(1),
		},
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
		combinedPrice() {
			return this.count
				? (this.count * this.currentItem.price).toFixed(2)
				: '';
		},
	},
	methods: {
		addToCart() {
			let formOutput = {
				item: this.currentItem.item,
				count: this.count,
				options: this.itemOptions,
				addOns: this.itemAddons,
				combinedPrice: this.combinedPrice,
			};

			let addOnError = this.$v.itemAddons.$invalid;
			let optionError = this.currentItem.options
				? this.$v.itemOptions.$invalid
				: false;
			let countError = this.$v.count.$invalid;

			if (addOnError || optionError || countError) {
				this.errors = true;
			} else {
				this.errors = false;
				this.cartSubmitted = true;
				this.$store.commit('addToCart', formOutput);
			}
		},
	},
};
</script>

<style scoped>
.container {
	width: 1000px;
	margin: 100px auto;
	display: grid;
	grid-template-columns: 400px 1fr;
	grid-template-rows: 400px 1fr;
	gap: 60px;
	line-height: 2;
}

.image {
	grid-area: 1 / 1 / 2 / 2;
	background-size: cover;
}

.details {
	grid-area: 1 / 2 / 2 / 3;
	position: relative;
}

.options {
	grid-area: 2 / 1 /3 / 2;
}
</style>
