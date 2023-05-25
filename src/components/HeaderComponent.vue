<template>
  <header class="header">
		<div class="container">
			<a class="header__logo" href="/" @click.prevent="false">
				<img src="../assets/logo.svg" alt="logo" width="40" height="40">
				{{ text }}
			</a>
			<div class="header__menu"></div>
		</div>
  </header>
</template>

<script setup>

const text = 'Filter CSS Generator (Beta)'
</script>