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
					The <a href="https://developer.mozilla.org/ru/docs/Web/CSS/filter" target="_blank">filter <TooltipComponent :text="tooltipText" class="filter__description-tooltip" /> </a> CSS property applies graphical effects like blur or color shift to an element. Filters are commonly used to adjust the rendering of images, backgrounds, and borders.
				</div>
				
			</div>

		</div>
	</section>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'
import vue3Slider from "vue3-slider"
import TooltipComponent from "./TooltipComponent.vue"

const tooltipText = 'jump to MDN documentation'
const copied = ref(false)
const handleScale = 2.4
const height = 8

const inputs = reactive([
	{ id: 'invert', label: 'Invert', min: 0, max: 100, value: 0, dimension: '%', startVal: 0 },
	{ id: 'contrast', label: 'Contrast', min: 0, max: 1000, value: 100, dimension: '%', startVal: 100 },
	{ id: 'opacity', label: 'Opacity', min: 0, max: 100, value: 100, dimension: '%', startVal: 100 },
	{ id: 'saturate', label: 'Saturate', min: 0, max: 1000, value: 100, dimension: '%', startVal: 100 },
	{ id: 'hue', label: 'Hue Rotate', min: 0, max: 360, value: 0, dimension: '°', startVal: 0 },
	{ id: 'brightness', label: 'Brightness', min: 0, max: 200, value: 100, dimension: '%', startVal: 100 },
	{ id: 'blur', label: 'Blur', min: 0, max: 10, value: 0, dimension: 'px', startVal: 0 },
	{ id: 'sepia', label: 'Sepia', min: 0, max: 100, value: 0, dimension: '%', startVal: 0 },
	{ id: 'grayscale', label: 'Grayscale', min: 0, max: 100, value: 0, dimension: '%', startVal: 0 }
])

const inputValues = computed(() => {
  return inputs.map(input => input.value)
})


const output = computed(() => {
	return {
		filter: `invert(${inputValues.value[0]}%) contrast(${inputValues.value[1]}%) opacity(${inputValues.value[2]}%) saturate(${inputValues.value[3]}%) hue-rotate(${inputValues.value[4]}deg) brightness(${inputValues.value[5]}%) blur(${inputValues.value[6]}px) sepia(${inputValues.value[7]}%) grayscale(${inputValues.value[8]}%)`
	}
})

const resetValues = () => {
	inputs.forEach(item => {
		item.value = item.startVal
	})
}

async function copyResult() {
	let copyText = `
	filter: ${output.value.filter};
	-webkit-filter: ${output.value.filter};
	-moz-filter: ${output.value.filter};
	`
	await navigator.clipboard.writeText(copyText)
	copied.value = true
	setTimeout(() => {
		copied.value = false
	}, 1500)
}
</script>