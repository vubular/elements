<template>
	<button type="button"
		class="button is-outlined is-danger"
		@click="doClick()"><i class="fa fa-archive"></i></button>
</template>
<script>
	export default {
		name: "Archive",
		props: {
			dialog: {
				type: Boolean,
				default: false
			}
		},
		methods: {
			doClick() {
				this.$emit("click");
				if(this.dialog) this.confirm();
			},
			confirm() {
				this.$buefy.dialog.confirm({
					title: "Archive item",
					message: "You are about to <b>archive</b> an item?<br/>Archiving will unlist item from references.",
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