<template>
	<div class="is-inline-block">
		<button v-if="!editRouter"
			type="button"
			class="button edit-button is-info is-small"
			@click="$emit('edit')">
			<span class="icon"><i class="fa fa-edit"></i></span>
			<span>Edit</span>
		</button>
		<template v-else>
			<router-link v-if="$route" :to="editRouter" class="button edit-button is-info is-small">
				<span class="icon"><i class="fa fa-edit"></i></span>
				<span>Edit</span>
			</router-link>
			<a v-else :href="editRouter" class="button edit-button is-info is-small">
				<span class="icon"><i class="fa fa-edit"></i></span>
				<span>Edit</span>
			</a>
		</template>
	</div>
</template>
<script>
	export default {
		name: "Edit",
		props: {
			id: {
				type: [String, Number]
			},
			to: String
		},
		computed: {
			editRouter() {
				if(this.to) return this.to;
				if(this.$route && this.id) return this.$route.fullPath + "/"+ this.id + "/edit";
				if(!this.$route && this.id) return "#/" + this.to + "/" + this.id + "/edit";
				return false;
			}
		}
	}
</script>