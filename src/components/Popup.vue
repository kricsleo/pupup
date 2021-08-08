<template>
  <div class="main"></div>
</template>

<script lang="ts">
import Vue, { PropType, VNode } from "vue";
import { ENUM_POPUP_TRIGGER } from "./helpers";

export default Vue.extend({
  name: "popup",
  props: {
    triggers: {
      type: Array as PropType<ENUM_POPUP_TRIGGER[]>,
      required: false,
      default: () => [ENUM_POPUP_TRIGGER.hover]
    },
    opened: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  data() {
    return {
      innerOpened: this.opened
    };
  },
  watch: {
    opened() {
      this.innerOpened = this.opened;
    }
  },
  render(h): VNode {
    const { $scopedSlots, triggers } = this;
    const children = $scopedSlots.default();
    const p;
    const toggleTrigger = () => (this.innerOpened = !this.innerOpened);
    triggers.forEach(t => children.addEventListener(t, toggleTrigger));
    return children;
  },
  beforeDestroy() {}
});
</script>

<style scoped lang="scss"></style>
