<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">
      View All
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >
      Completed
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    updateFilter(arg) {
      this.$emit("filterChange", arg);
    },
  },
};
</script>

<style>
.filter-nav button {
  all: unset;
  color: #bbb;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  font-weight: bold;
  letter-spacing: 1px;
  cursor: pointer;
}
.filter-nav button.active {
  color: #555;
}
</style>
