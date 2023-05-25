<template>
	<footer class="footer">
			<span>© 2023</span> | <a class="footer__link" :href="link" target="_blank">
				<IconGithub />
				<span>GitHub</span>
			</a>
		</footer>
</template>

<script>
import IconGithub from './icons/IconGithub.vue';


export default {
    data() {
        return {
            link: "https://github.com/Grinch3214"
        };
    },
    components: { IconGithub }
}
</script>