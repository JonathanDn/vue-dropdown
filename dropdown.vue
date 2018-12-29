<template>
	<div
		class="dropdown"
		@click="toggleRiskLevels"
		:class="{ expanded: isExpanded }"
		:style="[
      { '--options-height': optionsHeight + 'px' },
      { '--options-height-neg': '-' + optionsHeight + 'px' },
      { '--option-height': optionHeight + 'px' },
      { '--main-el-border-radius': borderRadius },
      { '--dropdown-width': width + 'px' },
      { '--dropdown-background-color': backgroundColor },
      { '--dropdown-expanded-color': backgroundExpandedColor },
      { '--dropdown-border': border },
      { '--dropdown-hover-background-color': hoverBackgroundColor },
      { '--dropdown-default-text-color': textColor }
    ]"
	>
		<div class="dropdown-label-container">
			<div class="dropdown-label">
        <span class="text">
          {{ (config.prefix ? config.prefix : "") + " "
          }}{{ config.placeholder ? config.placeholder : "" }}
        </span>
				<i class="angle-down" :class="{ toggled: isExpanded }"></i>
			</div>
		</div>

		<div v-expand="isExpanded" class="options expand">
			<div
				v-for="option in configOptions"
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
				width: 100,
				configOptions: [],
				backgroundColor: "#cde4f5",
				backgroundExpandedColor: "#fff",
				hoverBackgroundColor: "#0084d4",
				border: "1px solid  #232b35",
				borderRadius: 0,
				textColor: "#fff",
				isExpanded: false
			};
		},
		components: {},
		props: ["config"],
		computed: {},
		directives: {
			expand: {
				inserted: function(el, binding) {
					if (binding.value !== null) {
						function calcHeight() {
							const currentState = el.getAttribute("aria-expanded");
							el.classList.add("u-no-transition");
							el.removeAttribute("aria-expanded");
							el.style.height = null;
							el.style.height = el.clientHeight + "px";
							el.setAttribute("aria-expanded", currentState);

							setTimeout(function() {
								el.classList.remove("u-no-transition");
							});
						}
						el.classList.add("expand");
						el.setAttribute("aria-expanded", binding.value ? "true" : "false");
						calcHeight();
						window.addEventListener("resize", calcHeight);
					}
				},
				update: function(el, binding) {
					if (el.style.height && binding.value !== null) {
						el.setAttribute("aria-expanded", binding.value ? "true" : "false");
					}
				}
			}
		},
		methods: {
			toggleRiskLevels() {
				this.isExpanded = !this.isExpanded;
			},
			setCurrentSelectedOption(option) {
				this.$emit("setSelectedOption", option);
			},
			setConfigData() {
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
			},
			setOptionsHeight() {
				this.optionsHeight = this.optionHeight * this.configOptions.length;
			}
		},
		created() {
			this.setConfigData();
			this.setOptionsHeight();
		},
		beforeUdate() {
			// this.setOptionsHeight();
		},
		mounted() {}
	};
</script>

<style lang="scss" scoped>
	@import "./vue-dropdown";
</style>
