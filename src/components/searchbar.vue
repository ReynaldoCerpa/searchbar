<template>
  <div class="dropdown" v-if="options">

    <!-- Dropdown Input -->
    <input class="dropdown-input"
      :name="name"
      @focus="showOptions()"
      @blur="exit()"
      @keyup="keyMonitor"
      v-model="searchFilter"
      :disabled="disabled"
      :placeholder="placeholder" />
	  <div class="icon"/>

    <!-- Dropdown Menu -->
    <div class="dropdown-content"
      v-show="optionsShown">
      <div
        class="dropdown-item"
        @mousedown="selectOption(option)"
        v-for="(option, index) in filteredOptions"
        :key="index">
          {{ option.name || option.id || '-' }}
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Dropdown',
    template: 'Dropdown',
    props: {
      name: {
        type: String,
        required: false,
        default: 'dropdown',
        note: 'Input name'
      },
      options: {
        type: Array,
        required: true,
        default: [],
        note: 'Options of dropdown. An array of options with id and name',
      },
      placeholder: {
        type: String,
        required: false,
        default: 'Please select an option',
        note: 'Placeholder of dropdown'
      },
      disabled: {
        type: Boolean,
        required: false,
        default: false,
        note: 'Disable the dropdown'
      },
      maxItem: {
        type: Number,
        required: false,
        default: 6,
        note: 'Max items showing'
      }
    },
    data() {
      return {
        selected: {},
        optionsShown: false,
        searchFilter: ''
      }
    },
    created() {
      this.$emit('selected', this.selected);
    },
    computed: {
      filteredOptions() {
        const filtered = [];
        const regOption = new RegExp(this.searchFilter, 'ig');
        for (const option of this.options) {
          if (this.searchFilter.length < 1 || option.name.match(regOption)){
            if (filtered.length < this.maxItem) filtered.push(option);
          }
        }
        return filtered;
      }
    },
    methods: {
      selectOption(option) {
        this.selected = option;
        this.optionsShown = false;
        this.searchFilter = this.selected.name;
        this.$emit('selected', this.selected);
      },
      showOptions(){
        if (!this.disabled) {
          this.searchFilter = '';
          this.optionsShown = true;
        }
      },
      exit() {
        if (!this.selected.id) {
          this.selected = {};
          this.searchFilter = '';
        } else {
          this.searchFilter = this.selected.name;
        }
        this.$emit('selected', this.selected);
        this.optionsShown = false;
      },
      // Selecting when pressing Enter
      keyMonitor: function(event) {
        if (event.key === "Enter" && this.filteredOptions[0])
          this.selectOption(this.filteredOptions[0]);
      }
    },
    watch: {
      searchFilter() {
        if (this.filteredOptions.length === 0) {
          this.selected = {};
        } else {
          this.selected = this.filteredOptions[0];
        }
        this.$emit('filter', this.searchFilter);
      }
    }
  };
</script>


<style >
  .dropdown {
    position: relative;
    display: block;
	min-width: 250px;
	width: 100%;
	}
  .dropdown-input {
	background: #fff;
	cursor: pointer;
	border: 1px solid #bdbdbd;
	border-radius: 3px;
	color: #333;
	display: block;
	font-size: 1em;
	padding: 10px;
	min-width: 250px;
	width: 100%;
	outline: none;
	}
  .dropdown-content {
	background-color: #fff;
	min-width: 250px;
	max-height: 248px;
	border: 1px solid #e7ecf5;
	box-shadow: 0px -8px 34px 0px rgba(0,0,0,0.05);
	z-index: 1;
	}
  .dropdown-item {
	color: black;
	font-size: 1em;
	line-height: 1rem;
	padding: 8px;
	text-decoration: none;
	cursor: pointer;
  }
.dropdown-item:hover {
background-color: #bae3ff
}
  .dropdown:hover .dropdowncontent {
	display: block;
  }
.icon {
  background-image: url("https://icon-library.com/images/google-magnifying-glass-icon/google-magnifying-glass-icon-2.jpg");
  background-size: cover;
  width: 25px;
  height: 25px;
  position: absolute;
  top: 8px;
  right:-10px;

}
</style>
