<template>
    <select
    class="form-select w-25 my-3"
    aria-label="Default select example"
    :value="filtervalue"
    @change="handleFilterChange"
  >
    <option value="tutti">Tutte le carte</option>
    <option
      v-for="option in ArchetypeList"
      :key="option.id"
      :value="option.archetype"
    >
      {{ option.archetype }}
    </option>
  </select>
</template>

<script>
    export default {
  name: 'SelectComponet',
  props: {
    filtervalue: String,
    ArchetypeList: Array,
  },
  methods: {
    handleFilterChange(event) {
      this.$emit('filter-change', event.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>

</style>