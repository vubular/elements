<template>
	<button type="button"
		class="button is-danger"
		:class="{'is-outlined': dialog}"
		@click="doClick()"><slot><i class="fa fa-archive"></i></slot></button>
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
					confirmText: "Archive",
					type: "is-danger",
					hasIcon: true,
					icon: "archive fa-2x",
					iconPack: "fa",
					onConfirm: () =>  { this.$emit("archived") },
					onCancel: () =>  { this.$emit("canceled") }
				});
			}
		}
	}
</script>