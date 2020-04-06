<template>
	<div class="tabs is-fullwidth is-primary">
		<ul class="is-marginless">
			<li v-for="(tab, t) in tabs" :key="t"
				:class="{'is-active': activeTab==t}"
				@click="switchTab(tab, t)">
				<a v-html="tab"></a>
			</li>
			<li v-if="expandable" class="is-pulled-right has-text-right is-narrow">
				<i v-if="!expanded" @click="toggle" class="fal fa-lg fa-arrow-to-right expand-icon"></i>
				<i v-else @click="toggle" class="fal fa-lg fa-arrow-to-left expand-icon"></i>
			</li>
		</ul>
	</div>
</template>
<script>
	export default {
		name: 'Tabs',
		props: {
			tabs: {
				type: Array
			},
			expandable: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				activeTab: 0,
				expanded: false
			}
		},
		methods: {
			switchTab(label, index) {
				this.activeTab = index;
				this.$emit('active', label)
			},
			toggle() {
				this.$emit("expand");
				this.expanded = !this.expanded;
			}
		}
	}
</script>
<style scoped>
	.tabs li { margin-top: 0; }
	.tabs li a { color: #dbdbdb; }
	.tabs li a:hover { color: black; transition: color ease 1s; }
	.tabs li.is-active a { color: #7957d5; }
	.expand-icon { margin-right: 15px; cursor: pointer; color: #999; }
</style>