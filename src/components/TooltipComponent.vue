<template>
  <div class="tooltip">
		{{ text }}
	</div>
</template>


<script>

export default {
	name: 'TooltipComponent',
	props: {
		text: {
			type: String,
			default: 'Tooltip top'
		}
	}
}
</script>

<style lang="scss" scoped>
.tooltip {
	position: absolute;
	z-index: 10;
	bottom: calc(100% + 10px);
	left: 50%;
	transform: translateX(-50%);
	width: 150px;
	padding: 3px;
	color: var(--white-color);
	background: rgba(0, 0, 0, .6);
	font-size: .8rem;
	font-weight: 400;
	border-radius: var(--border-radius);
	cursor: default;
	pointer-events: none;
	display: none;

	&::before {
		content: '';
		position: absolute;
		top: 100%;
		left: 50%;
		transform: translateX(-50%);
		width: 0;
		height: 0;
		border-top: 6px solid rgba(0, 0, 0, 0.6);
		border-right: 6px solid rgba(0, 0, 0, 0);
		border-bottom: 6px solid rgba(0, 0, 0, 0);
		border-left: 6px solid rgba(0, 0, 0, 0);
	}
}
</style>