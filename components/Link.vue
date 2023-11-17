<template>
	<NuxtLink class="link">
		<slot></slot>
	</NuxtLink>
</template>

<style lang="scss" scoped>
@mixin link-hover-focus-styles {
	color: #fff;
	background-image: linear-gradient(to right, #1e59ff, #0db7eb,#ceff00, #0db7eb, #1e59ff);
	background-size: 400% .125em;
	animation: scroll-gradient 10s linear infinite;
}

.link {
	display: inline-block;
	background-image: linear-gradient(#9698c3, #9698c3);
	background-position: 0 calc(1.25em);
	background-repeat: repeat-x;
	background-size: 400% .0625em;
	color: #9698c3;
	transition-property: color, background-size;
	transition-duration: .2s;

	@keyframes scroll-gradient {
		to {
			background-position-x: 400%;
		}
	}

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
