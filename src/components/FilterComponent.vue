<template>
	<section class="filter">
		<div class="filter__container container">

			<div class="filter__group">
				<h2 class="filter__title">Filter Options</h2>
				<div v-for="input in inputs" :key="input.id" class="filter__slider">
					<div class="filter__desc">
						<label class="filter__desc-label" :for="input.id">{{ input.label }}</label>
						<p class="filter__desc-value">{{ input.value }}{{ input.dimension }}</p>
					</div>
					<div class="filter__input">
						<vue3-slider :id="input.id" :min="input.min" :max="input.max" v-model="input.value" color="var(--main-color)" trackColor="#a5a5a5" :height="height" :handleScale="handleScale" alwaysShowHandle />
					</div>
				</div>
			</div>

			<div class="filter__output">

				<div class="filter__image" :style="output">
					<img src="../assets/images/image.jpg" alt="" width="320" height="240">
				</div>

				<div class="filter__result">
					<p>filter: {{ output.filter }};</p>
					<p>-webkit-filter: {{ output.filter }};</p>
					<p>-moz-filter: {{ output.filter }};</p>
				</div>

				<div class="filter__copy">
					<button class="btn" @click="copyResult">
						<span v-if="!copied">Copy</span>
						<span v-else>Copied</span>
					</button>
					<button class="btn filter__copy-reset" @click="resetValues">Reset</button>
				</div>
				
				<div class="filter__description">
					The <a href="https://developer.mozilla.org/ru/docs/Web/CSS/filter" target="_blank">filter</a> CSS property applies graphical effects like blur or color shift to an element. Filters are commonly used to adjust the rendering of images, backgrounds, and borders.
				</div>
				
			</div>

		</div>
	</section>
</template>

<script>
import slider from "vue3-slider"

export default {
  components: {
		"vue3-slider": slider,
	},
	name: 'FilterComponent',
	data() {
    return {
			copied: false,
			handleScale: 2.4,
			height: 8,
      inputs: [
        { id: 'invert', label: 'Invert', min: 0, max: 100, value: 0, dimension: '%', startVal: 0 },
        { id: 'contrast', label: 'Contrast', min: 0, max: 1000, value: 100, dimension: '%', startVal: 100 },
        { id: 'opacity', label: 'Opacity', min: 0, max: 100, value: 100, dimension: '%', startVal: 100 },
				{ id: 'saturate', label: 'Saturate', min: 0, max: 1000, value: 100, dimension: '%', startVal: 100 },
				{ id: 'hue', label: 'Hue Rotate', min: 0, max: 360, value: 0, dimension: '°', startVal: 0 },
				{ id: 'brightness', label: 'Brightness', min: 0, max: 200, value: 100, dimension: '%', startVal: 100 },
				{ id: 'blur', label: 'Blur', min: 0, max: 10, value: 0, dimension: 'px', startVal: 0 },
				{ id: 'sepia', label: 'Sepia', min: 0, max: 100, value: 0, dimension: '%', startVal: 0 },
				{ id: 'grayscale', label: 'Grayscale', min: 0, max: 100, value: 0, dimension: '%', startVal: 0 }
      ]
    }
  },
	computed: {
    inputValues() {
      return this.inputs.map(input => input.value);
    },
		output() {
			return {
				filter: `invert(${this.inputValues[0]}%) contrast(${this.inputValues[1]}%) opacity(${this.inputValues[2]}%) saturate(${this.inputValues[3]}%) hue-rotate(${this.inputValues[4]}deg) brightness(${this.inputValues[5]}%) blur(${this.inputValues[6]}px) sepia(${this.inputValues[7]}%) grayscale(${this.inputValues[8]}%)`
			}
		}
  },
	methods: {
		resetValues() {
			this.inputs.forEach(item => {
				item.value = item.startVal
			})
		},

		async copyResult() {
			let copyText = `
			filter: ${this.output.filter};
			-webkit-filter: ${this.output.filter};
			-moz-filter: ${this.output.filter};
			`
			await navigator.clipboard.writeText(copyText)
			this.copied = true
			setTimeout(() => {
				this.copied = false
			}, 1500)
		}
	}
}
</script>