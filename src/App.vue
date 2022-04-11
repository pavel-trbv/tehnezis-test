<template>
  <div class="content">
    <TagList :tags="tags" :align="align" :tagTextWrap="tagTextWrap" />
  </div>
</template>

<script>
import TagList from './components/TagList.vue';

export default {
  name: 'App',

  components: {
    TagList,
  },

  data: () => ({
    tags: [],
    align: 'left',
    tagTextWrap: true,
  }),

  created() {
    this.getTags().then((tags) => {
      this.tags = tags;
    });
  },

  methods: {
    async getTags() {
      /**
       * something api call
       * e.g. const tags = await axios.get('/api/tags');
       */
      const tags = [
        {
          text: '4,3',
          icon: 'mdi-star-outline',
        },
        {
          text: 'Фридландские ворота',
        },
        {
          text: '1,2 км от вас',
        },
      ];

      return tags;
    },
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

body {
  color: #191919;
  font-size: 16px;
  font-family: 'Roboto', sans-serif;
}

.content {
  margin: 40px;
}
</style>
