<template>
	<div class="dropdown" @click="toggleRiskLevels"
	     :style="[{'--options-height': optionsHeight + 'px'},
	            {'--option-height': optionHeight + 'px'},
	            {'--dropdown-width': width + 'px'},
	            {'--dropdown-background-color': backgroundColor},
	            {'--dropdown-border' : border},
	            {'--dropdown-hover-background-color': hoverBackgroundColor},
	            {'--dropdown-default-text-color': textColor}]">
		<span class="text">{{(prefix ? prefix : "") + ' '}}{{placeholder}}</span>
		<i class="fa fa-angle-down"></i>
		<div v-if="isBottomSectionToggled"
		     class="options">
			<div v-for="option in configOptions"
			     class="option"
			     @click="setCurrentSelectedOption(option)">
				{{ option.value }}
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
				width: 100,
				configOptions: [],
				placeholder: "",
				prefix: "",
				backgroundColor: "transparent",
				hoverBackgroundColor: "#0084d4",
				border: "1px solid transparent",
				textColor: "#fff",
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
				this.width = this.config.width;
				this.placeholder = this.config.placeholder;
				if (this.config.prefix) {
					this.prefix = this.config.prefix;
				}
				if (this.config.backgroundColor) {
					this.backgroundColor = this.config.backgroundColor;
				}
				if (this.config.border) {
					this.border = this.config.border;
				}
				if (this.config.hoverBackgroundColor) {
					this.hoverBackgroundColor = this.config.hoverBackgroundColor;
				}
				if (this.config.textColor) {
					this.textColor = this.config.textColor;
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
