<template>
	<svg viewBox="0 0 458 458" xmlns="http://www.w3.org/2000/svg">
		<path d="M458 458L153.362 408.764C64.9785 394.539 0 318.337 0 228.928C0 139.508 64.9785 63.3172 153.351 49.0916L458 0V458Z" :fill="`url(#${id})`" />
		<defs>
			<linearGradient :id="id" x1="27" y1="229" x2="438" y2="229" gradientUnits="userSpaceOnUse">
				<stop :stop-color="color" />
				<stop offset="1" :stop-color="color" stop-opacity="0" />
			</linearGradient>
		</defs>
	</svg>
</template>

<script setup lang="ts">
import { nanoid } from 'nanoid';

defineProps<{
	color: string;
}>();

const id: string = `id-${nanoid()}`;
</script>
