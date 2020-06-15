<template>
	<div class="is-fullwidth color-picker-wrap">
		<button type="button"
			class="button is-medium color-picked"
			@click="pickColor"
			:style="pickedColorBackground"></button>
		<button v-if="ui.focus"
			type="button"
			class="button is-medium"
			@click="pickedColor">OK</button>
		<vue-color v-if="ui.focus"
			v-model="ui.color"
			:presetColors="ui.presets"
			@input="pushUpdates"
			:key="color"></vue-color>
	</div>
</template>
<script>
	export default {
		name: 'ColorPicker',
		props: {
			color: String
		},
		created() { if(this.color==null) { this.ui.color = this.getRandomHexColor(); this.pickedColor(); } },
		data() {
			return {
				ui: {
					color: null,
					presets: ['hsl(256, 60%, 59%)', 'hsl(204, 86%, 53%)', 'hsl(217, 71%, 53%)', 'hsl(141, 71%, 48%)', 'hsl(48, 100%, 67%)', 'hsl(348, 100%, 61%)', 'hsl(171, 100%, 41%)'],
					focus: false
				}

			}
		},
		methods: {
			pickColor() {
				this.ui.focus = true;
			},
			pickedColor() {
				this.$emit("picked", this.ui.color);
				this.ui.focus = false;
			},
			pushUpdates(value) {
				this.ui.color = value.hex;
			},
			getRandomHexColor() {
				var letters = '0123456789ABCDEF';
				var color = '#';
				for (var i = 0; i < 6; i++) {
					color += letters[Math.floor(Math.random() * 16)];
				}
				return color;
			}
		},
		computed: {
			pickedColorBackground: {
				cache: false,
				get() {
					return "background-color:" + this.ui.color + ";";
				}
			}
		},
		watch: {
			color(value) {
				if(value!=null) {
					this.ui.color = value;
				} else {
					this.ui.color = this.getRandomHexColor();
				}
			}
		}
	}
</script>
<style scoped>
	.color-picker-wrap { height: 45px; }
	button.color-picked { min-width: 100px; }
	>>> .vc-sketch { margin-left: 100px; z-index: 1; }
</style>