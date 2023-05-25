<template>
	<footer class="footer">
			<span>© 2023</span> | <a class="footer__link" :href="link" target="_blank">
				<IconGithub />
				<span>GitHub</span>
			</a>
		</footer>
</template>

<script setup>
import IconGithub from './icons/IconGithub.vue'

const link = 'https://github.com/Grinch3214'
</script>