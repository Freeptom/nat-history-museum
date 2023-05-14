<template>
  <article class="highlight">
    <div class="highlight-header">
      <div
        v-html="highlight.badge"
        class="highlight-header__badge"
      />
      <img
        class="highlight-header__image"
        :src="
          highlight.image?.source
            ? highlight.image?.source
            : `https://source.unsplash.com/random/?${stripSpaces(highlight.name)}`
        "
        :alt="highlight.image?.alt"
      />
    </div>
    <div
      class="highlight-body"
      :class="{ 'highlight-body--partner': highlight.isPartner }"
    >
      <h2 class="highlight-body__name">{{ highlight?.name }}</h2>
      <p class="highlight-body__date">
        Posted <time :datetime="highlight.date">{{ formatDate(highlight.date) }}</time>
      </p>
      <p class="highlight-body__description">
        {{ highlight?.description }}
      </p>
      <div
        v-if="highlight.news"
        class="highlight-body__news"
      >
        <strong>{{ newsDate }}</strong>
        <p>{{ highlight.news.title }}</p>
      </div>
      <div
        v-if="uniqueData.length"
        class="highlight-body__additional"
      >
        <h3>More Info:</h3>
        <div
          v-for="(item, index) in uniqueData"
          :key="index"
        >
          <template v-if="isUrl(item.value)">
            <a :href="item.value"> {{ item.value }}</a>
          </template>
          <template v-else>
            <div>{{ item.value }}</div>
          </template>
        </div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  name: "MuseumHighlight",
  props: {
    highlight: {
      type: Object,
    },
  },
  computed: {
    newsDate() {
      return this.highlight.news.date
        ? `News - ${this.formatDate(this.highlight.news.date)}`
        : "News";
    },
    uniqueData() {
      let relatedData = [];
      const categoryType = this.highlight.uniqueData[this.highlight.type];
      Object.keys(categoryType).forEach((key) => {
        if (categoryType[key]) {
          relatedData.push({
            name: key,
            value: categoryType[key],
          });
        }
      });
      return relatedData;
    },
  },
  methods: {
    stripSpaces(string) {
      return string.replace(/\s/g, "");
    },
    isUrl(string) {
      const urlPattern = new RegExp(
        "^(https?:\\/\\/)?" +
          "((([a-z\\d]([a-z\\d-]*[a-z\\d])*)\\.)+[a-z]{2,}|" +
          "((\\d{1,3}\\.){3}\\d{1,3}))" +
          "(\\:\\d+)?(\\/[-a-z\\d%_.~+]*)*" +
          "(\\?[;&a-z\\d%_.~+=-]*)?" +
          "(\\#[-a-z\\d_]*)?$",
        "i"
      );
      return !!urlPattern.test(string);
    },

    formatDate(inputDate) {
      const toDate = new Date(inputDate);
      let date, month, year;

      date = toDate.getDate();
      month = toDate.getMonth() + 1;
      year = toDate.getFullYear();

      date = date.toString().padStart(2, "0");
      month = month.toString().padStart(2, "0");

      return `${date}/${month}/${year}`;
    },
  },
};
</script>

<style lang="scss" scoped>
.highlight {
  position: relative;
  display: flex;
  flex-direction: column;
}
.highlight-header {
  display: flex;
  flex-direction: column;
  &__badge {
    position: absolute;
    top: -1rem;
    right: -0.5rem;
    font-size: 1.75rem;
    color: white;
  }
  &__image {
    border-radius: var(--border-radius) var(--border-radius) 0 0;
    width: 100%;
    height: 200px;
    object-fit: cover;
    object-position: center;
  }
}
.highlight-body {
  flex: 1;
  padding: 1em;
  background: var(--clr-card-primary);
  border-radius: 0 0 var(--border-radius) var(--border-radius);
  &--partner {
    background: var(--clr-card-highlight);
  }
  &__date,
  &__description {
    margin-bottom: 1rem;
  }
  &__date {
    font-size: 0.875rem;
  }
  &__news {
    border-radius: calc(var(--border-radius) * 2);
    background: var(--clr-news-bg);
    border: 1px solid var(--clr-news-border);
    padding: 1rem;
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  }
  &__additional {
    padding-block: 2rem;
  }
}
</style>
