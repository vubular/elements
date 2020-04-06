<template>
	<section class="hero is-white">
		<div class="hero-body" :class="[!subtitleText || compact ? 'compact': '', '']">
			<div class="columns is-mobile">
				<div class="column is-4-mobile is-narrow">
					<i v-if="iconClass" :class="iconClass" class="is-size-2-mobile"></i>
				</div>
				<div class="column">
					<h1 class="title is-size-4-mobile" v-html="titleText"></h1>
					<h2 class="subtitle is-size-6-mobile" v-if="subtitleText">{{subtitleText}}</h2>
				</div>
			</div>
		</div>
	</section>
</template>
<script>
	export default {
		name: 'Hero',
		props: {
			icon: {
				type: String
			},
			type: {
				type: String,
				default: null
			},
			title: {
				type: String
			},
			subtitle: {
				type: String,
				default: ''
			},
			compact: {
				type: Boolean,
				default: false
			}
		},
		computed: {
			iconClass() {
				return (this.icon) ? this.icon : this.$route.meta.hero.icon;
			},
			titleText() {
				return (this.title) ? this.title : this.$route.meta.hero.title;
			},
			subtitleText() {
				if(this.subtitle!='') return this.subtitle;
				if(this.$route.meta && this.$route.meta.hero && this.$route.meta.hero.subtitle) return this.$route.meta.hero.subtitle;
				return "";
			}
		}
	};
</script>
<style scoped>
	.hero-body i { font-size: 64px; float:left; margin: 0 40px; }
	.hero { margin-bottom: 20px; border-radius: 5px; }
	.hero.is-white { box-shadow: 0px 0px 0px 1px rgba(0,0,0,0.1); }
	.hero-body.compact { padding: 1.5rem; }
	.hero-body.compact i { font-size: 40px; margin: 0 20px; }
	.hero-body.compact .column .title { font-weight: 300; margin: 0; }
	.is-danger-dark { background-color: #c54d65; color: #fff; }
	.is-danger-dark h1, .is-danger-dark h2 { color: #fff; }
</style>