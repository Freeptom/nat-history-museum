<template>
  <div class="page">
    <h1 class="page__title">{{ type }}</h1>
    <div class="page__highlights">
      <MuseumHighlight
        v-for="highlight in sortedHighlights"
        :key="highlight.date"
        :highlight="highlight"
      >
      </MuseumHighlight>
    </div>
  </div>
</template>

<script>
import MuseumHighlight from "./MuseumHighlight";

export default {
  name: "MuseumPage",
  components: {
    MuseumHighlight,
  },
  props: {
    type: {
      type: String,
      validator(value) {
        return ["space", "dinosaurs", "oceans", "wildlife"].includes(value);
      },
    },
    highlights: {
      type: Array,
    },
  },
  computed: {
    sortedHighlights() {
      const items = this.highlights;
      return items.sort((a, b) => (new Date(a.date) > new Date(b.date) ? -1 : 1));
    },
  },
};
</script>

<style lang="scss" scoped>
.page {
  width: max(500px, 90%);
  padding: 2em;

  &__title {
    color: #2c3791;
    font-size: 1.5rem;
    font-weight: 600;
    margin-bottom: 1rem;
  }

  &__highlights {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 2rem;
  }
}
</style>
