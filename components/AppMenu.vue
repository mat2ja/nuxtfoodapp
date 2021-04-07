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
		<NuxtLink to="/cart">Cart</NuxtLink>
	</nav>
</template>

<script>
import AppLogo from '@/components/AppLogo.vue';

export default {
	components: {
		AppLogo,
	},
};
</script>

<style scoped>
</style>