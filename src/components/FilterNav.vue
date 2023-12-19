<template>
  <nav class="filter-nav">
    <button
      class="filter-btn"
      @click="filterNavStatus('all')"
      :class="{ active: this.current === 'all' }"
    >
      ALl
    </button>
    <button
      class="filter-btn"
      @click="filterNavStatus('ongoing')"
      :class="{ active: this.current === 'ongoing' }"
    >
      ongoing
    </button>
    <button
      class="filter-btn"
      @click="filterNavStatus('complete')"
      :class="{ active: this.current === 'complete' }"
    >
      complete
    </button>
  </nav>
  <!-- {{ this.current }} -->
</template>

<script>
export default {
  props: ["current"],
  methods: {
    filterNavStatus(value) {
      this.$emit("filterProjects", value);
    },
  },
};
</script>

<style>
.filter-nav {
  margin: 50px 0 10px 0;
}
.filter-nav button {
  font-size: 15px;
  font-weight: bold;
  margin: 20px 10px 10px 0;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #aaa;
  background: none;
  outline: none;
  display: inline;
  padding: 0;
  cursor: pointer;
}
button.active {
  color: black;
}
</style>
