<template>
	<button type="button"
		class="button is-outlined is-danger"
		@click="doClick()"><i class="fal fa-archive"></i></button>
</template>
<script>
	export default {
		name: 'Archive',
		methods: {
			doClick() {
				this.$emit('click');
			}
		}
	}
</script>