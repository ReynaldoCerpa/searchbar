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
</div>
</template>

<script>
import Dropdown from "@/components/searchbar"
export default {
  name: 'App',
  components: {
	Dropdown
  }
}
</script>

<style>
.container {
width: 5rem;
}
</style>
