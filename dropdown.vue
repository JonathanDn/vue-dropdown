<template>
	<div
		class="dropdown"
		@click.stop="checkDropdownHandler"
		:class="computedClasses"
		:style="computedStyles"
	>
		<div class="dropdown-label-container">
			<div class="dropdown-label">
				<span class="text">
					{{ (config && config.prefix ? config.prefix : "") + " "
					}}{{ config && config.placeholder ? config.placeholder : placeholder }}
				</span>
				<i class="angle-down" :class="{ toggled: isExpanded }"></i>
			</div>
		</div>

		<div v-expand="isExpanded" class="options expand">
			<div
				v-for="(i, option) in configOptions"
				:key="'option-' + i"
				class="option"
				@click="setCurrentSelectedOption(option);"
			>
				{{ option.value }}
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: "dropdown",
		data() {
			return {
				isBottomSectionToggled: false,
				optionsHeight: 0,
				optionHeight: 35,
				configOptions: [
					{
						value: "option 1"
					},
					{
						value: "option 2"
					},
					{
						value: "option 3"
					}
				],
				backgroundColor: "#cde4f5",
				backgroundExpandedColor: "#fff",
				hoverBackgroundColor: "#0084d4",
				disabledBackgroundColor: "#ccc",
				disabledTextColor: "#555",
				isExpanded: false,
				placeholder: "Placeholder",
				textColor: "black",
				borderRadius: "1.5em",
				border: "1px solid gray",
				width: 180
			};
		},
		components: {},
		props: ["config"],
		computed: {
			computedStyles: function () {
				return [
					{"--options-height": this.optionsHeight + "px"},
					{"--options-height-neg": "-" + this.optionsHeight + "px"},
					{"--option-height": this.optionHeight + "px"},
					{"--main-el-border-radius": this.borderRadius},
					{"--dropdown-width": this.width + "px"},
					{"--dropdown-background-color": this.config.disabled ? this.disabledBackgroundColor : this.backgroundColor},
					{"--dropdown-expanded-color": this.backgroundExpandedColor},
					{"--dropdown-border": this.border},
					{"--dropdown-hover-background-color": this.hoverBackgroundColor},
					{"--dropdown-default-text-color":  this.config.disabled ? this.disabledTextColor : this.textColor}
				];
			},
			computedClasses: function() {
				return { 
					'expanded': this.isExpanded, 
					'disabled': this.config.disabled 
				}
			}
		},
		directives: {
			expand: {
				inserted: function (el, binding) {
					if (binding.value !== null) {
						function calcHeight() {
							const currentState = el.getAttribute("aria-expanded");
							el.classList.add("u-no-transition");
							el.removeAttribute("aria-expanded");
							el.style.height = null;
							el.style.height = el.clientHeight + "px";
							el.setAttribute("aria-expanded", currentState);

							setTimeout(function () {
								el.classList.remove("u-no-transition");
							});
						}

						el.classList.add("expand");
						el.setAttribute("aria-expanded", binding.value ? "true" : "false");
						calcHeight();
						window.addEventListener("resize", calcHeight);
					}
				},
				update: function (el, binding) {
					if (el.style.height && binding.value !== null) {
						el.setAttribute("aria-expanded", binding.value ? "true" : "false");
					}
				}
			}
		},
		methods: {
			toggleDropdownOptions() {
				this.isExpanded = !this.isExpanded;
			},
			setCurrentSelectedOption(option) {
				this.$emit("setSelectedOption", option);
			},
			setConfigData() {
				if (this.config) {
					this.configOptions = this.config.options;
					this.width = this.config.width;
					this.placeholder = this.config.placeholder;
					if (this.config.backgroundColor) {
						this.backgroundColor = this.config.backgroundColor;
					}
					if (this.config.backgroundExpandedColor) {
						this.backgroundExpandedColor = this.config.backgroundExpandedColor;
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
					if (this.config.borderRadius) {
						this.borderRadius = this.config.borderRadius;
					}
				}
			},
			setOptionsHeight() {
				this.optionsHeight = this.optionHeight * this.configOptions.length;
			},
			documentClicked() {
				if (this.isExpanded) {
					this.isExpanded = false
				}
			}, 
			checkDropdownHandler() {
				if (!this.config.disabled) {
					this.toggleDropdownOptions()
				} 
			},
		},
		created() {
			document.addEventListener('click', this.documentClicked);
			this.setConfigData();
			this.setOptionsHeight();
		},
		beforeUdate() {
			// this.setOptionsHeight();
		},
		destroyed() {
			document.removeEventListener('click', this.documentClicked);
		}
	};
</script>

<style lang="scss" scoped>
	@import "./dropdown";
</style>
