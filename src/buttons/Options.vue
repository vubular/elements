<template>
	<div class="columns is-multiline">
		<div v-if="label && label!='hide'" class="column is-12" style="padding: 30px 0 0 50px">
			<h3 class="subtitle is-3 has-text-weight-light">{{label}}</h3>
		</div>
		<div class="column is-12">
			<div class="columns is-multiline">
				<template v-for="(option, o) in options">
					<slot name="option" :option="{index: o, fields:option}">
						<div class="column option-buttons">
							<button type="button"
								class="button is-large option-button"
								:class="{'is-primary': selectedOption==option}"
								v-fawesome="option.icon"
								@click="selectOption(option)">
								<span>{{option.label}}</span>
							</button>
							<h4 class="subtitle is-4" v-html="option.description"></h4>
						</div>
					</slot>
				</template>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: "Options",
		props: {
			label: String,
			options: Array
		},
		data() {
			return {
				selectedOption: null
			}
		},
		methods: {
			selectOption(option) {
				this.$emit("selected", option);
				this.selectedOption = option;
			}
		}
	}
</script>
<style scoped>
	button.option-button { padding: 50px; height: auto; }
	button.option-button:hover { background-color: #7957d5; color: #fff; }
	.columns .column.option-buttons { padding: 50px; }
	.columns .column.option-buttons .button { margin-bottom: 30px; margin-bottom: 50px; }
	.columns .column.option-buttons h3 { font-weight: 200; padding: 30px; padding-bottom: 0; padding-left: 0; }
	.columns .column.option-buttons h4 { font-weight: 200; padding: 30px;  padding-top: 0; padding-left: 0; }
	.columns .column.option-buttons { padding-bottom: 0; }
</style>