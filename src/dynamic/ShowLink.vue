<template>
	<router-link :to="routerLinkTo">
		<slot v-if="$slots.default[0] && $slots.default[0].text!=''"></slot>
		<plain v-else>{{noLabel}}</plain>
	</router-link>
</template>
<script>
	export default {
		name: 'ShowLink',
		props: {
			to: {
				type: String,
				default: null
			},
			id: {
				type: [String, Number],
				default: null
			}
		},
		computed: {
			routerLinkTo() {
				if(this.to) return this.to;
				var routerLinkTo = "";
				var routePath = this.$route.path.replace(/\/$/, "");
					routePath = routePath.split('/');
					routerLinkTo = routePath[routePath.length-1];
				var routerID = null;
				if(this.id) routerID = this.id;
				if(!this.id && this.$slots.default[0].text && this.$slots.default[0].text!="Undefined") {
					routerID = this.$slots.default[0].text;
				}
				routerLinkTo += "/" + routerID;

				return routerLinkTo;
			},
			noLabel() {
				return this.$i18n ? this.$t("- Undefined -") : "- Undefined -";
			}
		}
	}
</script>