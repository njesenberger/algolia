<template>
	<section class="introduction-section" v-if="!animationEnded" ref="introductionSection">
		<div class="introduction-spotlight-container">
			<Spotlight class="introduction-spotlight" color="var(--primary-color-2)" />
			<div class="introduction-spotlight-base"></div>
		</div>
		<form class="introduction-form" @submit.prevent>
			<div class="introduction-search-bar-container">
				<svg class="introduction-search-bar-icon" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
					<path fill-rule="evenodd" clip-rule="evenodd" d="M4 11C4 7.13401 7.13401 4 11 4C14.866 4 18 7.13401 18 11C18 12.886 17.2541 14.5978 16.0412 15.8566C16.0071 15.8828 15.9742 15.9116 15.9429 15.9429C15.9116 15.9742 15.8828 16.0071 15.8566 16.0412C14.5978 17.2541 12.886 18 11 18C7.13401 18 4 14.866 4 11ZM16.6177 18.0319C15.078 19.2635 13.125 20 11 20C6.02944 20 2 15.9706 2 11C2 6.02944 6.02944 2 11 2C15.9706 2 20 6.02944 20 11C20 13.125 19.2635 15.078 18.0319 16.6177L21.7071 20.2929C22.0977 20.6834 22.0977 21.3166 21.7071 21.7071C21.3166 22.0977 20.6834 22.0977 20.2929 21.7071L16.6177 18.0319Z" />
				</svg>
				<label class="visually-hidden" for="search">Search</label>
				<input class="introduction-search-bar" v-model="search" id="search" type="search" placeholder="Search…" readonly>
			</div>
			<button class="introduction-search-button" ref="button" type="submit" disabled>Search</button>
		</form>
	</section>
</template>

<script lang="ts" setup>
const search: Ref<string> = ref('');
const finalSearch: string = 'Nicolas Jesenberger';
const animationEnded: Ref<boolean> = ref(false);

const introductionSection: Ref<HTMLElement | null> = ref(null);
const button: Ref<HTMLButtonElement | null> = ref(null);

onMounted(() => {
	document.body.classList.add('no-scroll');
	introductionSection.value!.classList.add('spotlight-on');
	setTimeout(() => {
		let i: number = 0;
		const interval: NodeJS.Timeout = setInterval(() => {
			search.value += finalSearch[i];
			i += 1;
			if (i === finalSearch.length) {
				clearInterval(interval);
				setTimeout(() => {
					button.value!.classList.add('animate');
					button.value!.addEventListener('animationend', () => {
						introductionSection.value!.classList.add('animation-ended');
						introductionSection.value!.addEventListener('transitionend', () => {
							animationEnded.value = true;
							document.body.classList.remove('no-scroll');
						}, { once: true });
					});
				}, 250);
			}
		}, 50);
	}, 1500);
});
</script>

<style lang="scss" scoped>
.introduction-section {
	display: flex;
	align-items: center;
	justify-content: center;
	position: fixed;
	inset: 0;
	background-color: var(--neutral-color-4);
	transition-property: transform, opacity;
	transition-duration: .5s;

	&.animation-ended {
		transform: scale(1.5);
		opacity: 0;
	}
}

.introduction-spotlight-container {
	position: fixed;
	z-index: -1;
	inset: 0;
	opacity: 0;
	transition: opacity 1s cubic-bezier(1, .125, 1, 0);

	.introduction-section.spotlight-on & {
		opacity: .25;
	}
}

.introduction-spotlight {
	position: absolute;
	z-index: -1;
	top: 0;
	left: 50%;
	transform: translateX(-50%) rotate(90deg);
	height: 75vh;
	min-height: 428px;
}

.introduction-spotlight-base {
	position: absolute;
	z-index: -1;
	top: max(75vh, 428px);
	left: 50%;
	transform: translateX(-50%);
	width: 75vh;
	height: 12vh;
	min-width: 428px;
	background-image: radial-gradient(closest-side, var(--primary-color-2), var(--primary-color-2-alpha-0));
}

.introduction-form {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	row-gap: 2em;
	filter: brightness(.25);
	transition: filter 1s cubic-bezier(1, .125, 1, 0);

	.introduction-section.spotlight-on & {
		filter: brightness(1);
	}
}

.introduction-search-bar-container {
	display: flex;
	align-items: center;
	column-gap: .5em;
	border: 1px solid var(--primary-color-3);
	border-radius: 50px 12px 12px 50px;
	padding: .5em 1em;
	min-width: 16em;
	box-shadow:
		inset -6px 0 12px var(--primary-color-4),
		inset 6px 0 12px var(--primary-color-4);
	cursor: default;
}

.introduction-search-bar-icon {
	width: 1.5em;
	height: 1.5em;
	fill: var(--primary-color-3);
}

.introduction-search-bar {
	color: var(--neutral-color-1);
	cursor: default;
}

.introduction-search-button {
	border-radius: 8px 50px 50px 8px;
	padding: .5em 1em;
	min-width: 10em;
	background-image: linear-gradient(180deg, var(--primary-color-1), var(--primary-color-3) 62%, var(--primary-color-2));
  box-shadow:
    inset 0 1px 0 rgb(255 255 255 / .2),
    inset 0 -1px 0 rgb(0 0 0 / .6),
    0 1px 2px rgb(0 0 0 / .2);
	text-align: center;
	color: var(--neutral-color-1);
	text-shadow: 0 1px rgba(0 0 0 / .2);
	animation: button-click .5s paused;
	cursor: default;

	&.animate {
		animation-play-state: running;
	}
}

@keyframes button-click {
	25% {
		transform: scale(1.04);
		filter: brightness(1.2);
	}
	75% {
		transform: scale(.92);
		filter: brightness(.8);
	}
	100% {
		transform: scale(1);
		filter: brightness(1);
	}
}
</style>
