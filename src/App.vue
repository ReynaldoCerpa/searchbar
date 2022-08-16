<template>
<div class="container">
<Dropdown
    :options="[{ id: 1, name: 'Option 1'}, { id: 2, name: 'Option 2'}]"
    v-on:selected=""
    v-on:filter=""
    :disabled="false"
    name="zipcode"
    :maxItem="10"
    placeholder="Search by CPN">
</Dropdown>
<button @click="printData"/>
</div>
</template>

<script>
import Dropdown from "@/components/searchbar"
export default {
  name: 'App',
  components: {
	Dropdown
  },
methods: {
		   printData() {
		   console.log(this.selected)
		   }
		 }
}
</script>

<style>
.container {
width: 9rem;
}
</style>
