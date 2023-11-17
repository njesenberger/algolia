<template>
	<slot></slot>
	<div class="background-spotlights-container">
		<Spotlight class="background-spotlight" color="var(--primary-color-2)" />
		<Spotlight class="background-spotlight" color="var(--secondary-color-pink-1)" />
	</div>
</template>

<style lang="scss">
:root {
	color-scheme: dark;
}

::selection {
	background-color: var(--primary-color-2);
	color: var(--neutral-color-1);
}

body {
	margin: 0 auto;
	padding: 120px 24px 3em;
	max-width: 35em;
	min-height: 100vh;
	min-height: 100dvh;
	background-color: var(--neutral-color-4);
	color: var(--neutral-color-2);
	font-feature-settings: 'tnum';
	font-variant-numeric: tabular-nums;

	&.no-scroll {
		overflow: hidden;
	}
}

.background-spotlights-container {
	position: fixed;
	z-index: -1;
	inset: 0;
	opacity: .25;
}

.background-spotlight {
	position: absolute;
	top: 50%;
	left: 50%;
	height: 100vh;
	min-height: 680px;

	&:nth-child(1) {
		transform: translate(-50%, -75%);
	}

	&:nth-child(2) {
		transform: translate(-50%, -25%) rotate(180deg);
	}
}
</style>
