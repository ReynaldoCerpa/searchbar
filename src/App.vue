<template>
<div class="container">
<Dropdown
    :options="[{ id: 1, name: 'Option 1'}, { id: 2, name: 'Option 2'}]"
	v-on:selected="validateSelection"
    v-on:filter="getDropdownValues"
    :disabled="false"
    name="zipcode"
    :maxItem="10"
    placeholder="Search by CPN">
</Dropdown>
<button @click="printData">Print data</button>
</div>
</template>

<script>
import Dropdown from "@/components/searchbar"
export default {
  name: 'App',
		  data() {
			return {
			selected: {name:null, id:null}
			}
		  },
  components: {
	Dropdown
  },
methods: {
		   printData() {
		   console.log(this.selected.name)
		   },
validateSelection(selection) {
            this.selected = selection;
            console.log(selection.name+' has been selected');
          },
          getDropdownValues(keyword) {
            console.log('You could refresh options by querying the API with '+keyword);
          }		 }
}
</script>

<style>
.container {
width: 9rem;
}
</style>
