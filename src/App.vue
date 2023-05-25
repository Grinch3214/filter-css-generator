<template>
  <HeaderComponent />

  <main>
		<FilterComponent />
  </main>

	<FooterComponent />
</template>


<script setup>
import FilterComponent from './components/FilterComponent.vue'
import FooterComponent from './components/FooterComponent.vue'
import HeaderComponent from './components/HeaderComponent.vue'
</script>