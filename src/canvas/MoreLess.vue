<template>
	<div class="column">
		<div v-if="mode=='display'" class="columns">
			<div v-show="expandable && !isExpanded" class="column is-narrow">
				<slot name="expand-button">
					<button type="button" class="button" @click="expand">More</button>
				</slot>
			</div>
			<div v-show="isExpanded" class="column">
				<slot></slot>
			</div>
			<div v-show="shrinkable && isExpanded" class="column is-narrow">
				<slot name="shrink-button">
					<button type="button" class="button" @click="shrink">Less</button>
				</slot>
			</div>
		</div>
		<div v-if="mode=='render'" class="columns">
			<div v-if="expandable && !isExpanded" class="column is-narrow">
				<slot name="expand-button">
					<button type="button" class="button" @click="expand">More</button>
				</slot>
			</div>
			<div v-if="isExpanded" class="column">
				<slot></slot>
			</div>
			<div v-if="shrinkable && isExpanded" class="column is-narrow">
				<slot name="shrink-button">
					<button type="button" class="button" @click="shrink">Less</button>
				</slot>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'MoreLess',
		props: {
			mode: {
				type: String,
				default: 'display'
			},
			expanded: {
				type: Boolean,
				default: false
			},
			shrinked: {
				type: Boolean,
				default: true
			},
			expandable: {
				type: Boolean,
				default: true
			},
			shrinkable: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				isExpanded: false
			}
		},
		created() {
			if(this.expanded || !this.shrinked) this.isExpanded = true;
		},
		methods: {
			expand() {
				this.$emit("expanded");
				this.isExpanded = true;
			},
			shrink() {
				this.$emit("shrinked");
				this.isExpanded = false;
			}
		}
	}
</script>