<template>
  <ons-popover v-on="unrecognizedListeners">
    <slot></slot>
  </ons-popover>
</template>

<script>
  import { hidable, hasOptions, dialogCancel, deriveEvents, deriveDBB, portal } from '../mixins';

  export default {
    mixins: [hidable, hasOptions, dialogCancel, deriveEvents, deriveDBB, portal],

    props: {
      target: {
        validator(value) {
          return value._isVue || typeof value === 'string' || value instanceof Event || value instanceof HTMLElement;
        }
      }
    },

    computed: {
      normalizedTarget() {
        if (this.target && this.target._isVue) {
          return this.target.$el;
        }
        return this.target;
      },
      normalizedOptions() {
        if (this.target) {
          return {
            target: this.normalizedTarget,
            ...this.options
          };
        }
        return this.options;
      }
    }
  };
</script>
