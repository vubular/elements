<script>
	export default {
		name: 'Trim',
		props: {
			text: {
				type: String
			},
			characters: {
				type: Array,
				default() {
					return [' ']
				}
			}
		},
		render() {
			return this._v(this.content);
		},
		computed: {
			content: {
				cache: false,
				get() {
					var content = '';
					if(this.text) content = this.text;
					if(this.$slots.default[0] && this.$slots.default[0].text) content = this.$slots.default[0].text;

					if(typeof content == 'string') {
						for(var c in this.characters) {
							var char = this.characters[c];
							content = content.split(char).join('');
						}
					}

					return content;
				}
			}
		}
	}
</script>