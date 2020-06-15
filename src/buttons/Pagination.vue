<template>
	<nav class="pagination">
		<ul class="pagination-list">
			<li  @click="switchPage(activePage-10)" :class="{'disabled': activePage<11}">
				<a class="pagination-link"><i class="fal fa-chevron-double-left"></i></a>
			</li>
			<li @click="switchPage(activePage-1)" :class="{'disabled': activePage==1}">
				<a class="pagination-link"> <i class="fal fa-chevron-left"> </i> Prev</a>
			</li>
			<li v-for="page in total" :key="page" v-if="Math.abs(page - activePage) < 3 || page == total || page == 1" :class="{current: activePage === page, last: (page == total && Math.abs(page - activePage) > 3), first:(page == 1 && Math.abs(page - activePage) > 3)}">
				<a class="pagination-link"
					:class="{'is-current': activePage==page}"
					@click="switchPage(page)" v-text="page"></a>
			</li>
			<li @click="switchPage(activePage+1)" :class="{'disabled': activePage == total}">
				<a class="pagination-link">Next</span> <i class="fal fa-chevron-right"></i></a>
			</li>
			<li @click="switchPage(activePage+10)" :class="{'disabled': activePage > total-10}">
				<a class="pagination-link"><i class="fal fa-chevron-double-right"></i></a>
			</li>
		</ul>
	</nav>
</template>
<script>
	export default {
		name: 'Pagination',
		props: {
			active: Number,
			total: {
				type: Number,
				default: 1
			}
		},
		data() {
			return {
				activePage: 1
			}
		},
		methods: {
			switchPage(page) {
				this.activePage = page;
				this.$emit('active', page)
			}
		},
		watch: {
			active: function (newValue, oldValue) {
				if(newValue && newValue!=oldValue && typeof newValue === 'number' && newValue!=this.activePage) {
					this.switchPage(newValue);
				}
			}
		}
	}
</script>
<style scoped>
	nav.pagination { border:0 !important;padding:0 !important; }
	ul.pagination-list { margin:0 !important; list-style-type: none; }
	ul.pagination-list li { list-style-type: none; margin-top: 0; }
	.fa-chevron-right { margin-left:10px; }
	.fa-chevron-left { margin-right:10px; }
	.fa-chevron-right, .fa-chevron-left, .fa-chevron-double-left, .fa-chevron-double-right { font-size: 12px; }

	li.first::after {
  		content:'...';
  		vertical-align: bottom;
  		color: rgba(0,0,0,.7);
  		padding: 7px;
  		position: relative;
  		bottom: 5px;
	}

	li.last::before {
		content:'...';
  		vertical-align: bottom;
	 	color: rgba(0,0,0,.7);
	 	padding: 7px;
	 	position: relative;
	 	bottom: 5px;
	}
	.disabled {
	    pointer-events:none;
	    cursor: not-allowed!important;
	    opacity: 0.4;
	}
</style>