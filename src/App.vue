<template>
  <HeaderComponent />

  <main>
		<FilterComponent />
  </main>

	<FooterComponent />
</template>


<script>
import FilterComponent from './components/FilterComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
import HeaderComponent from './components/HeaderComponent.vue';
export default {
	name: 'App',
	components: {
    FilterComponent,
    HeaderComponent,
		FooterComponent
	}
}
</script>