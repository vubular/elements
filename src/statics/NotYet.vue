<template v-if="wrap=='table'">
	<td colspan="9999" class="has-text-grey-light has-text-centered">
		<slot>{{'No items yet.' | translate}}</slot>
	</td>
</template>
<template v-else>
	<slot>{{'No items yet.' | translate}}</slot>
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