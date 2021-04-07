<template>
	<main class="container cart">
		<h2>Your Cart</h2>

		<table v-if="cart.length">
			<thead>
				<th>Item</th>
				<th>AddOns</th>
				<th>Amount</th>
				<th>Total Price</th>
			</thead>

			<tbody>
				<tr v-for="item in cart" :key="item.id">
					<td>
						{{ item.item }}
						<span v-if="item.options.length > 0"
							>- {{ item.options }}</span
						>
					</td>
					<td>
						<span
							class="comma"
							v-for="addOn in item.addOns"
							:key="addOn"
							>{{ addOn }}</span
						>
					</td>
					<td>{{ item.count }}</td>
					<td>${{ item.combinedPrice }}</td>
				</tr>
				<tr>
					<td colspan="3"></td>
					<td class="total">Total: ${{ totalPrice }}</td>
				</tr>
			</tbody>
		</table>
		<AppCartEmpty v-else />
	</main>
</template>

<script>
import { mapState } from 'vuex';
import { mapGetters } from 'vuex';
import AppCartEmpty from '@/components/AppCartEmpty.vue';

export default {
	components: {
		AppCartEmpty,
	},
	computed: {
		...mapState(['cart']),
		...mapGetters(['totalPrice']),
	},
};
</script>
 
