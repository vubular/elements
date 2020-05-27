<template>
	<div class="date-tip">
		<template v-if="compact">
			<b-tooltip :label="theTime" position="is-right" type="is-dark">{{theDate}}</b-tooltip>
		</template>
		<template v-else>{{theDate}}</template>
	</div>
</template>
<script>
	export default {
		name: 'DateTip',
		props: {
			date: { type: [String, Object] },
			compact: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				parsedDate: null
			}
		},
		beforeMount() {
			if(!this.date) {
				if(this.$slots.default && this.$slots.default[0] && this.$slots.default[0].text) {
					this.parsedDate = new Date(Date.parse(this.$slots.default[0].text));
				} else {
					this.parsedDate = new Date();
				}
			} else {
				if(String(this.date)) { this.parsedDate = new Date(Date.parse(this.date)); }
				if(typeof this.date =='object' && this.date.created_at) { this.parsedDate = new Date(Date.parse(this.date.created_at)); }
			}
		},
		computed: {
			theDate() {
				var ymd = [];
				ymd.push(this.parsedDate.getFullYear());
				ymd.push(this.parsedDate.getMonth()+1);
				ymd.push(this.parsedDate.getDate());
				for(var d in ymd) { if(ymd[d]<10) { ymd[d] = "0"+ ymd[d]; } }

				if(this.compact) { return ymd.reverse().join("."); }

				return ymd.reverse().join(".") +" "+ this.theTime;
			},
			theTime() {
				var his = [];
				his.push(this.parsedDate.getHours());
				his.push(this.parsedDate.getMinutes());
				his.push(this.parsedDate.getSeconds());
				for(var s in his) { if(his[s]<10) { his[s] = "0"+ his[s]; } }

				return his.join(":");
			}
		}
	};
</script>