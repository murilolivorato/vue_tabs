<template>
  <div className="tab-content" v-show="value === selectedTitle">
    <slot></slot>
  </div>
</template>
<script>
import {inject} from 'vue'

export default {
  props: ['title', 'value', 'active'],
  setup() {
    const selectedTitle = inject('selectedTitle')
    return {
      selectedTitle
    }
  }
}
</script>
