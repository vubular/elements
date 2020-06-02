<template>
	<div class="date-tip">
		{{theDate}} <span v-if="compact" class="time-tip">{{theTime}}</span>
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
			this.parseDate(this.date);
		},
		computed: {
			theDate: {
				cache: false,
				get() {
					var ymd = [];
					if(this.parsedDate) {
						ymd.push(this.parsedDate.getFullYear());
						ymd.push(this.parsedDate.getMonth()+1);
						ymd.push(this.parsedDate.getDate());
					}
					for(var d in ymd) { if(ymd[d]<10) { ymd[d] = "0"+ ymd[d]; } }
					if(this.compact) { return ymd.reverse().join("."); }
					return ymd.reverse().join(".") +" "+ this.theTime;
				}
			},
			theTime: {
				cache: false,
				get() {
					var his = [];
					if(this.parsedDate) {
						his.push(this.parsedDate.getHours());
						his.push(this.parsedDate.getMinutes());
						his.push(this.parsedDate.getSeconds());
					}
					for(var s in his) { if(his[s]<10) { his[s] = "0"+ his[s]; } }
					return his.join(":");
				}
			}
		},
		watch: {
			"date": {
				handler(newValue, oldValue) {
					if(newValue && newValue!=oldValue) {
						this.parseDate(newValue);
					}
				},
				deep: true
			}
		},
		methods: {
			parseDate(date) {
				this.parsedDate = new Date();
				if(date && typeof date == 'string') { this.parsedDate = new Date(Date.parse(date)); }
				if(date && typeof date =='object' && date.created_at) { this.parsedDate = new Date(Date.parse(date.created_at)); }
				if(date && typeof date =='object' && date.updated_at) { this.parsedDate = new Date(Date.parse(date.updated_at)); }
			}
		}
	};
</script>
<style scoped>
	.date-tip { position: relative; display: inline-block; }
	.date-tip .time-tip { visibility: hidden; max-width: 250px; background-color: #555; color: #fff; text-align: center; padding: 4px 8px !important; border-radius: 5px; position: absolute; z-index: 1; top: -5px; left: 115%; opacity: 0; transition: opacity 0.175s; }
	.date-tip .time-tip::after { content: ""; position: absolute; top: 50%; right: 100%; margin-top: -5px; border-width: 5px; border-style: solid; border-color: transparent #555 transparent transparent; }
	.date-tip:hover .time-tip { visibility: visible; opacity: 1; }
</style>