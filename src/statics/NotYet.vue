<template>
	<td colspan="9999" class="has-text-grey-light has-text-centered">
		<slot>
			<span class="icon"><i class="fal fa-empty-set"></i></span>
			<span>{{'No items yet.' | translate}}</span>
		</slot>
	</td>
</template>
<script>
	export default {
		name: "NotYet",
		props: {
			wrap: {
				type: String,
				default: "table"
			}
		}
	}
</script>