<template>
	<button type="button"
		class="button is-danger"
		:class="{'is-outlined': dialog}"
		@click="doClick()"><slot><i :class="icon"></i></slot></button>
</template>
<script>
	export default {
		name: "Archive",
		props: {
			dialog: {
				type: Boolean,
				default: false
			},
			title: {
				type: String,
				default: "Archive item"
			},
			message: {
				type: String,
				default: "You are about to <b>archive</b> an item?<br/>Archiving will unlist item from references."
			},
			button: {
				type: String,
				default: "Archive"
			},
			icon: {
				type: String,
				default: "fa fa-archive"
			}
		},
		methods: {
			doClick() {
				if(this.dialog) {
					this.$emit("click");
					this.confirm();
				} else {
					this.$emit("archived");
				}
			},
			confirm() {
				this.$buefy.dialog.confirm({
					title: this.title,
					message: this.message,
					confirmText: this.button,
					type: "is-danger",
					hasIcon: true,
					icon: this.icon.split(" ").pop().replace("fa-","") + " fa-2x",
					iconPack: "fa",
					onConfirm: () =>  { this.$emit("archived") },
					onCancel: () =>  { this.$emit("canceled") }
				});
			}
		}
	}
</script>