<template>
  <div id="app">
    <MuseumPage
      :type="type"
      :highlights="normalisedHighlights"
    />
  </div>
</template>

<script>
import MuseumPage from "./components/MuseumPage.vue";

export default {
  name: "App",
  components: {
    MuseumPage,
  },
  data() {
    return {
      type: "space",
      spaceHighlights: [
        {
          date: "2020-04-20 12:20:00",
          description:
            "Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.",
          id: 1,
          image: "",
          name: "Asteroids",
        },
        {
          date: "2020-05-20 15:50:00",
          description:
            "A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.",
          id: 9,
          image: "",
          name: "Comets",
        },
        {
          date: "2020-05-01 9:22:00",
          description:
            "The term planet is ancient, with ties to history, astrology, science, mythology, and religion.",
          id: 7,
          image: "",
          name: "Planets",
          news: {
            date: "2020-08-18 18:00:00",
            title: "Attend our talk about Jupiter with Dr. Hogarth",
          },
          quiz: "https://planetquiz.space",
        },
        {
          date: "2020-07-05 4:10:00",
          description:
            "A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.",
          id: 12,
          image: "",
          name: "Meteor showers",
          news: {
            title: "The Lyrids will peak at on April 21-22 2021, at night",
          },
        },
      ],
      spacePartners: {
        observatory: {
          createdAt: "2020-06-01 11:45:00",
          info: "The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.",
          image: "",
          name: "Mauna Kea Observatories",
        },
      },
    };
  },
  computed: {
    normalisedHighlights() {
      const items = [];
      const joinedData = {
        ...this.spacePartners,
        ...this.spaceHighlights,
      };

      Object.keys(joinedData).forEach((key) => {
        const item = joinedData[key];
        items.push({
          type: this.type,
          name: item?.name,
          id: item?.id,
          image: {
            source: item?.image,
            alt: item?.name,
          },
          date: item?.date || item?.createdAt,
          description: item?.description || item?.info,
          news: item?.news,
          isPartner: !!item?.info,
          badge: this.badge,
          uniqueData: {
            space: {
              quiz: item?.quiz ?? null,
            },
            dinosaur: {
              period: item?.period ?? null,
            },
            wildlife: {
              location: item?.location ?? null,
              species: item?.species ?? null,
              status: item?.status ?? null,
            },
          },
        });
      });
      return items;
    },
    badge() {
      const badges = {
        space: "&#11088;",
        dinosaurs: `<img src="/dinosaur.png"  height=50 width=50/>`,
        // further images
        oceans: "",
        wildlife: "",
      };
      return badges[this.type];
    },
  },
};
</script>

<style>
:root {
  --clr-card-primary: #f3f4f6;
  --clr-card-highlight: #ffe4e6;
  --clr-news-border: #d1d5db;
  --clr-news-bg: #e8eaef;
  --border-radius: 0.25rem;
}
#app {
  display: flex;
  justify-content: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
img {
  max-width: 100%;
}
h1,
h2,
h3,
h4,
h5,
h6,
p {
  margin: 0;
}
p {
  margin: 0;
}
</style>
