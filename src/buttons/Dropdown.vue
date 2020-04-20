<template>
	<div class="dropdown is-right" :class="{'is-active': isFocused}" v-on-clickaway="blur">
		<div class="dropdown-trigger">
			<slot name="trigger" v-bind="{focus, isFocused}">
				<button type="button" class="button is-small" @click="focus">
					<span class="icon" v-fawesome="'fal fa-ellipsis-h'"></span>
				</button>
			</slot>
		</div>
		<div class="dropdown-menu" id="dropdown-menu" role="menu">
			<div class="dropdown-content">
				<slot v-bind="{blur, isFocused}"></slot>
			</div>
		</div>
	</div>
</template>
<script>
	import { mixin as clickaway } from 'vue-clickaway';
	export default {
		name: "Dropdown",
		mixins: [ clickaway ],
		data() {
			return {
				isFocused: false
			}
		},
		methods: {
			focus() {
				if(!this.isFocused) {
					this.isFocused = true;
					this.$emit("focus");
				} else {
					this.blur();
				}
			},
			blur() {
				if(this.isFocused) {
					this.isFocused = false;
					this.$emit("blur");
				}
			}
		}
	}
</script>