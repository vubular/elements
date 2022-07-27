<template>
	<div class="is-fullwidth" :class="{'precond': !condition,'no-border': noBorder}">
		<slot v-if="condition"></slot>
		<div v-else class="columns disfocus">
			<div v-if="!silent" class="column is-1 has-text-really-centered"><i :class="icon"></i></div>
			<div v-if="!silent" class="column is-11">
				<p class="subtitle is-3 has-text-grey" style="font-weight:200;margin:0" v-html="title"></p>
				<p class="subtitle is-4 has-text-grey-light" style="font-weight:200;margin:0" v-html="description"></p>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: "Conditional",
		props: {
			condition: [ Boolean, String, Number, Object, Array, Date ],
			icon: {
				type: String,
				default: "fal fa-divide fa-3x fa-border"
			},
			title: {
				type: String,
				default: "Please try filling other requirements until this section reveals."
			},
			description: {
				type: String,
				default: "Contents here are conditioned by surrounding elements above or below."
			},
			noBorder: Boolean,
			silent: Boolean
		}
	}
</script>
<style scoped>
	.precond { margin-top: 30px; }
	.precond.no-border { margin-top: 0; }
	.precond .columns { border-top: 1px solid #f3f3f3; }
	.precond.no-border .columns { border: 0; }
	.precond .columns .column { padding: 30px; }
	.precond .columns.disfocus { opacity: .5; transition: all .5s ease-in-out; }
	.precond .columns.disfocus:hover { opacity: 1; }
	.fa-divide { color: #eee !important; }
</style>