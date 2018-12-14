<template>
	<div class="dropdown" @click="toggleRiskLevels"
	     :style="[{'--options-height': optionsHeight + 'px'},
	            {'--option-height': optionHeight + 'px'},
	            {'--dropdown-width': dropdownWidth + 'px'},
	            {'--dropdown-background-color': dropdownBackgroundColor},
	            {'--dropdown-border' : dropdownBorder},
	            {'--dropdown-hover-background-color': dropdownHoverBackgroundColor},
	            {'--dropdown-default-text-color': dropdownTextColor}]">
		<span class="text">{{(prefix ? prefix : "") + ' '}}{{placeholder}}</span>
		<i class="fa fa-angle-down"></i>
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
				prefix: "",
				dropdownBackgroundColor: "transparent",
				dropdownHoverBackgroundColor: "#0084d4",
				dropdownBorder: "1px solid transparent",
				dropdownTextColor: "#fff",
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
				if (this.config.backgroundColor) {
					this.dropdownBackgroundColor = this.config.backgroundColor;
				}
				if (this.config.dropdownBorder) {
					this.dropdownBorder = this.config.dropdownBorder;
				}
				if (this.config.dropdownHoverBackgroundColor) {
					this.dropdownHoverBackgroundColor = this.config.dropdownHoverBackgroundColor;
				}
				if (this.config.dropdownTextColor) {
					this.dropdownTextColor = this.config.dropdownTextColor;
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
