<template>
	<div :class="ddClass" v-on-clickaway="blur">
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
		props: {
			position: {
				type: String,
				default: 'is-right'
			}
		},
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
			},
		},
		computed: {
			ddClass() {
				var ddClass = "dropdown";
				if(this.isFocused) ddClass = ddClass + " is-active"
				if(this.position) ddClass = ddClass + " " + this.position;
				return ddClass;
			}
		}
	}
</script>