<template>
	<NuxtLink class="link">
		<slot></slot>
	</NuxtLink>
</template>

<style lang="scss" scoped>
@mixin link-hover-focus-styles {
	color: var(--neutral-color-1);
	background-image: var(--primary-gradient);
	background-size: var(--primary-gradient-size-x) .125em;
	animation: scroll-primary-gradient 10s linear infinite;
}

.link {
	display: inline-block;
	background-image: linear-gradient(var(--neutral-color-2), var(--neutral-color-2));
	background-position: 0 calc(1.25em);
	background-repeat: repeat-x;
	background-size: var(--primary-gradient-size-x) .0625em;
	color: var(--neutral-color-2);
	transition-property: color, background-size;
	transition-duration: .2s;

	@media (hover: hover) {
		&:hover {
			@include link-hover-focus-styles;
		}
	}

	&:focus-visible {
		@include link-hover-focus-styles;
	}
}
</style>
