<template>
  <div class="pagination">
    <button v-for="page in pagesCount" :key="page">
      {{ page }}
    </button>
  </div>
</template>

<script>
export default {
  name: 'Pagination',
  props: {
    itemsCount: {
      type: Number,
    },
  },
  data() {
    return {
      pagesCount: null,
      countItemOfPage: 5,
    };
  },
  methods: {
    generatePages() {
      return Math.ceil(this.itemsCount / this.countItemOfPage);
    },
  },
  created() {
    this.pagesCount = this.generatePages();
  },
};
</script>

<style lang="scss"></style>
