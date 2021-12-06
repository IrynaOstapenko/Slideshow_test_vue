<template>
	<div class="slideshow">
		<div class="slideshow__buttons">
			<button @click="previousImage" class="slideshow__button">&lt;</button>
			<button @click="nextImage" class="slideshow__button">&gt;</button>
		</div>

		<div class="slideshow__extra">
			<button class="slideshow__button-caption" @click="showCaption = !showCaption">i</button>
		</div>

		<div class="slideshow__slides">
			<figure class="slideshow__slide">
				<img class="slideshow__img" :src="currentSlide.file" :alt="currentSlide.title">
				<figcaption v-if="showCaption" class="slideshow__caption">{{ currentSlide.caption }}</figcaption>
			</figure>
		</div>

		<div class="slideshow__dots">
			<button class="slideshow__dot" @click="goToIndex(index)" v-for="(slide, index) in slides" :aria-label="`Go to image ${index + 1}`"></button>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				index: 0,
				showCaption: false,
				slides: [
					{ title: 'Cat', caption: 'Meow meow', file: '/images/cat.jpeg' },
					{ title: 'Surf', caption: 'Surfs up', file: '/images/surf.jpeg' },
					{ title: 'Dog', caption: 'Woof woof', file: '/images/dog.jpeg' },
				],
			};
		},

		computed: {
			currentSlide() {
				return this.slides[this.index];
			}
		},

		methods: {
			previousImage() {
				this.index = (this.index === 0) ? this.slides.length - 1 : this.index - 1;
			},

			nextImage() {
				this.index = (this.index === this.slides.length - 1) ? 0 : this.index + 1;
			},

			goToIndex(index) {
				this.index = index;
			}
		}
	};
</script>

<style>
	.slideshow {
		position: relative;
		width: 80vw;
		height: 80vh;
		background: #eee;
	}

	.slideshow:hover .slideshow__caption {
		opacity: 1;
	}

	.slideshow__slides {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}

	.slideshow__slide {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	.slideshow__img {
		width: 100%;
		height: 100%;
		object-fit: contain;
	}

	.slideshow__caption {
		position: absolute;
		left: 0;
		bottom: 0;
		width: 100%;
		text-align: center;
		font-size: 0.75em;
		padding: 0.5em;
		background: pink;
	}

	.slideshow__extra {
		position: absolute;
		top: 0;
		left: 0;
		z-index: 10;
	}

	.slideshow__button-caption {
		padding: 0.5em;
		color: blue;
	}

	.slideshow__buttons {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: 10;
		display: flex;
		justify-content: space-between;
	}

	.slideshow__button {
		padding: 0.5em;
		text-transform: uppercase;
		color: blue;
		align-self: center;
	}

	.slideshow__dots {
		position: absolute;
		bottom: 0;
		transform: translateY(100%);
		display: flex;
		flex-flow: row nowrap;
		justify-content: center;
		padding: 0.5em;
		width: 100%;
	}

	.slideshow__dot {
		--dot-size: 0.8em;
		min-width: var(--dot-size);
		min-height: var(--dot-size);
		display: block;
		background: blue;
		border-radius: 100%;
	}

	.slideshow__dot + .slideshow__dot {
		margin-left: 0.5em;
	}
</style>
