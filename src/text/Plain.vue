<script>
	export default {
		name: 'Plain',
		props: {
			text: {
				type: String
			}
		},
		render() {
			return this._v(this.content);
		},
		computed: {
			content: {
				cache: false,
				get() {
					if(this.text) return this.text;
					if(this.$slots && this.$slots.default && Array.isArray(this.$slots.default) && this.$slots.default[0] && this.$slots.default[0].text) return this.$slots.default[0].text;
					return '';
				}
			}
		}
	}
</script>