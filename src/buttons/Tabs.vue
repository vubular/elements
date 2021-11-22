<template>
	<div class="tabs is-fullwidth is-primary">
		<ul class="is-marginless">
			<template v-for="(tab, t) in tabs">
				<li v-if="JSON.stringify(tab)[0]=='{'"
					:key="t"
					:class="{'is-active': activeTab==t}"
					@click="switchTabObject(tab, t)">
					<a>
						<span v-if="tab.icon" class="icon"><i :class="tab.icon"></i></span>
						<span v-if="tab.label">{{tab.label}}</span>
						<plain v-if="!tab.icon && !tab.label">{{tab}}</plain>
					</a>
				</li>
				<li v-else
					:key="t"
					:class="{'is-active': activeTab==t}"
					@click="switchTab(tab, t)">
					<a v-html="tab" v-if="!withIcons"></a>
					<a v-if="withIcons">
						<span v-if="tab=='Dashboard'">
							<i class="fa fa-home"></i>
							{{tab}}
						</span>	
						<span v-for="icon in installedApps">
							<span v-if="icon.namespace==tab">
								<i :class="icon.icon"></i> 
								<span> 
									{{tab}} 
								</span>
							</span>
						</span>
					</a>	
				</li>
			</template>
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
			tabs: Array,
			expandable: {
				type: Boolean,
				default: false
			},
			withIcons: {
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
			switchTabObject(tab, index) {
				this.activeTab = index;
				if(tab.label) {
					this.$emit('active', tab.label);
				} else {
					this.$emit('active', tab);
				}
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
	.tabs.capitalize li a { text-transform: capitalize; }
	.expand-icon { margin-right: 15px; cursor: pointer; color: #999; }
</style>