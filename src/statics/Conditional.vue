<template>
	<div class="is-fullwidth" :class="{'precond': !condition}">
		<slot v-if="condition"></slot>
		<div v-else class="columns disfocus">
			<div class="column is-1 has-text-really-centered">
				<i class="fal fa-divide fa-3x fa-border"></i>
			</div>
			<div class="column is-11">
				<p class="subtitle is-3 has-text-grey" style="font-weight:200;margin:0">
					Please try filling other requirements until this section reveals.
				</p>
				<p class="subtitle is-4 has-text-grey-light" style="font-weight:200;margin:0">
					Contents here are conditioned by surrounding elements above or below.
				</p>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: "Conditional",
		props: ["condition", "icon", "title", "description", "bordered"]
	}
</script>
<style scoped>
	.precond { margin-top: 30px; }
	.precond .columns { border-top: 1px solid #f3f3f3; }
	.precond .columns .column { padding: 30px; }
	.precond .columns.disfocus { opacity: .5; transition: all .5s ease-in-out; }
	.precond .columns.disfocus:hover { opacity: 1; }
	.fa-divide { color: #eee !important; }
</style>