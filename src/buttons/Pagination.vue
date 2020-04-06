<template>
	<nav class="pagination">
		<ul class="pagination-list">
			<li @click="switchPage(activePage-1)" :class="{'disabled': activePage==1}">
				<a class="pagination-link"> <i class="far fa-long-arrow-left">&nbsp;</i> Prev</a>
			</li>
			<li  @click="switchPage(activePage-10)" :class="{'disabled': activePage<11}">
				<a class="pagination-link"> << </a>
			</li>
			<li v-for="page in total" :key="page" v-if="Math.abs(page - activePage) < 3 || page == total || page == 1" :class="{current: activePage === page, last: (page == total && Math.abs(page - activePage) > 3), first:(page == 1 && Math.abs(page - activePage) > 3)}">
				<a class="pagination-link"
					:class="{'is-current': activePage==page}"
					@click="switchPage(page)" v-text="page"></a>
			</li>
			<li @click="switchPage(activePage+10)" :class="{'disabled': activePage > total-10}">
				<a class="pagination-link"> >> </a>
			</li>
			<li @click="switchPage(activePage+1)" :class="{'disabled': activePage == total}">
				<a class="pagination-link">Next</span>&nbsp;<i class="far fa-long-arrow-right"></i></a>
			</li>
		</ul>
	</nav>
</template>
<script>
	export default {
		name: 'Pagination',
		props: {
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
		}
	}
</script>
<style scoped>
	ul.pagination-list { margin:0 !important; list-style-type: none; }
	ul.pagination-list li { list-style-type: none; margin-top: 0; }

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