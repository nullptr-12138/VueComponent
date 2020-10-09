<template>
  <b-link class="link" @click="doPost">
    <slot></slot>
  </b-link>
</template>

<script>
import HttpRequestUtils from '../../assets/js/HttpRequestUtils'
import {hasError} from '../../assets/js/ErrorMessage'

export default {
  name: 'base-link',
  props: {
    url: {
      type: String,
      required: true
    },
    params: {
      type: Object,
      default: undefined
    },
    message: {
      type: String,
      default: ''
    }
  },
  methods: {
    doPost () {
      if (this.params === undefined) {
        HttpRequestUtils.doPostWithoutParams(this.url,
          response => this.callback(response))
      } else {
        HttpRequestUtils.doPostWithFormParams(this.url, this.param,
          response => this.callback(response))
      }
    },
    callback (response) {
      if (!hasError(response)) {
        if (this.message !== '') {
          alert(this.message)
        } else {
          this.$emit('success')
        }
      }
    }
  }
}
</script>

<style src="../../assets/css/link.less" lang="less" scoped>

</style>
