<template>
  <div class="filter">
    Filter items:
    <select @change="filterTodos($event)">    
      <option value="5">5</option>
      <option value="10">10</option>
      <option value="50">50</option>
      <option value="100">100</option>
    </select>
  </div>
</template>

<script>

import { mapActions } from "vuex";

export default {
    name: "FilterTodos",
    methods : mapActions(["filterTodos"])
};
</script>

<style>

.filter{
    padding-bottom: 10px;
}

</style>