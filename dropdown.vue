<template>
	<div class="dropdown" @click="toggleRiskLevels"
	     :style="[{'--options-height': optionsHeight + 'px'},
	            {'--option-height': optionHeight + 'px'},
	            {'--dropdown-width': dropdownWidth + 'px'}]">
		<span class="text">{{(prefix ? prefix : "") + ' '}}{{placeholder}}</span>
		<i class="fa fa-caret-down"></i>
		<div v-if="isBottomSectionToggled"
		     class="options">
			<div v-for="option in configOptions"
			     class="option"
			     @click="setCurrentSelectedOption(option)">
				{{option.value | firstLetterUpperCase}}
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'dropdown',
		data() {
			return {
				isBottomSectionToggled: false,
				optionsHeight: 0,
				optionHeight: 35,
				dropdownWidth: 100,
				configOptions: [],
				placeholder: "",
				prefix: ""
			}
		},
		components: {

		},
		props: ["config"],
		computed: {

		},
		methods: {
			toggleRiskLevels() {
				this.isBottomSectionToggled = !this.isBottomSectionToggled;
			},
			setCurrentSelectedOption(option) {
				this.$emit('setSelectedOption', option)
			},
			setConfigData() {
				this.configOptions = this.config.options;
				this.dropdownWidth = this.config.width;
				this.placeholder = this.config.placeholder;
				if (this.config.prefix) {
					this.prefix = this.config.prefix;
				}
			},
			setOptionsHeight() {
				this.optionsHeight = this.optionHeight * this.configOptions.length;
			},
		},
		created() {
			this.setConfigData();
			this.setOptionsHeight();
		},
		mounted() {

		}
	}
</script>

<style lang="scss" scoped>
	@import './dropdown';
</style>
