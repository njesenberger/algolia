<template>
	<NuxtLayout>
		<Heading class="heading-1">404 — Page not found</Heading>
		<Link to="/">Go back to homepage</Link>
	</NuxtLayout>
</template>

<script lang="ts" setup>
useHead({
	title: '404 — Page not found',
	bodyAttrs: {
		class: 'error',
	},
});
</script>

<style lang="scss">
.error {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	padding-top: 3em;
}
</style>
