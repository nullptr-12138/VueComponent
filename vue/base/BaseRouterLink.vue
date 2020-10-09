<template>
  <b-link class="link"
          :to="this.params === undefined ? this.url : {name: this.url, params: this.params}">
    <slot></slot>
  </b-link>
</template>

<script>
export default {
  name: 'base-router-link',
  props: {
    url: {
      type: String,
      required: true
    },
    params: {
      type: Object,
      default: undefined
    }
  }
}
</script>

<style src="../../assets/css/link.less" lang="less" scoped>

</style>
