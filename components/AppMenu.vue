<template>
	<nav>
		<ul>
			<li>
				<NuxtLink exact to="/">
					<AppLogo />
				</NuxtLink>
			</li>
			<li><NuxtLink to="/restaurants">Restaurants</NuxtLink></li>
		</ul>
		<div class="smallnum" v-if="cartCount > 0">{{ cartCount }}</div>
		<NuxtLink to="/cart">Cart</NuxtLink>
	</nav>
</template>

<script>
import AppLogo from '@/components/AppLogo.vue';
import { mapGetters } from 'vuex';

export default {
	components: {
		AppLogo,
	},
	computed: {
		...mapGetters(['cartCount']),
	},
};
</script>

<style scoped>
</style>