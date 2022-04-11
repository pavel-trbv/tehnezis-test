<template>
  <div
    class="tags"
    :class="{ 'tags--align-left': align === 'left', 'tags--align-breadth': align === 'breadth' }"
  >
    <template v-for="(tag, index) in tags">
      <TagItem :key="'tag' + index" :text="tag.text" :icon="tag.icon" :textWrap="tagTextWrap" />
      <div class="tags__separator" :key="'sep' + index" v-if="index !== tags.length - 1" />
    </template>
  </div>
</template>

<script>
import TagItem from './TagItem.vue';

export default {
  name: 'TagList',

  components: {
    TagItem,
  },

  props: {
    /**
     * Array of tag objects
     * @example [ { text: 'some text', icon: 'icon-name' } ]
     */
    tags: {
      type: Array,
      default: () => [],
    },

    /**
     * The align of tag list
     * @values left, breadth
     */
    align: {
      type: String,
      default: 'left',
    },

    /**
     * whether the text in the tag should wrap
     * @values true, false
     */
    tagTextWrap: {
      type: Boolean,
      default: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.tags {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 12px;

  &--align-left {
    justify-content: flex-start;
  }

  &--align-breadth {
    justify-content: space-between;
  }

  &__separator {
    display: none;
  }

  @media (min-width: 400px) {
    flex-flow: row wrap;
    align-items: center;

    &__separator {
      display: block;
      width: 4px;
      height: 4px;
      background-color: #191919;
      border-radius: 50%;
    }
  }
}
</style>
