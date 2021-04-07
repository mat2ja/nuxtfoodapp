<template>
	<main class="container cart">
		<h2>Cart</h2>
		<div v-for="item in $store.state.cart" :key="item.id">
			<pre>{{ item }}</pre>
		</div>
	</main>
</template>

<script>
export default {};
</script>

