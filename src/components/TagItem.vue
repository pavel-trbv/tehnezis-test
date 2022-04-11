<template>
  <div class="tag" :class="{ 'tag--visible': visible, 'tag--text-wrap': textWrap }" ref="tag">
    <v-icon v-if="icon" color="#191919" class="tag__icon">{{ icon }}</v-icon>
    <span class="tag__text">
      {{ text }}
    </span>
  </div>
</template>

<script>
import _ from 'lodash';

export default {
  name: 'TagItem',

  props: {
    /**
     * Tag text
     */
    text: String,
    /**
     * Icon name from MDI
     */
    icon: String,

    /**
     * whether the text in the tag should wrap
     * @values true, false
     */
    textWrap: Boolean,
  },

  data: () => ({
    visible: true,
  }),

  methods: {
    onResize() {
      if (this.el.clientWidth > this.parent.clientWidth && this.visible) {
        this.visible = false;
      } else if (this.el.clientWidth < this.parent.clientWidth && !this.visible) {
        this.visible = true;
      }
    },
  },

  mounted() {
    this.el = this.$refs.tag;
    this.parent = this.el.parentNode;
    this.onResizeDebounced = _.debounce(this.onResize, 300);

    this.onResizeDebounced();
    window.addEventListener('resize', this.onResizeDebounced);
  },

  destroyed() {
    window.removeEventListener('resize', this.onResizeDebounced);
  },
};
</script>

<style lang="scss">
.tag {
  display: none;
  flex-flow: row nowrap;
  align-items: center;
  white-space: nowrap;
  column-gap: 4px;

  &--visible {
    display: flex;
  }

  &--text-wrap {
    white-space: normal;
  }

  &__text {
    font-size: 18px;
  }
}
</style>
