<template>
	<nav>
		<ul>
			<li><NuxtLink exact to="/">Home</NuxtLink></li>
			<li><NuxtLink to="/restaurants">Restaurants</NuxtLink></li>
		</ul>
		<NuxtLink to="/cart">Cart</NuxtLink>
	</nav>
</template>

<script>
export default {};
</script>

<style scoped>
nav {
	height: 30px;
}
</style>