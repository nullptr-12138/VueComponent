<template>
    <b-modal ok-title="是" cancel-title="否" centered hide-backdrop
             v-model="showModal" @ok="onOk" @cancel="onCancel">
        <slot></slot>
    </b-modal>
</template>

<script>
import HttpRequestUtils from '../../assets/js/HttpRequestUtils'
import {hasError} from '../../assets/js/ErrorMessage'

export default {
  name: 'base-modal',
  model: {
    prop: 'show',
    event: 'show'
  },
  props: {
    show: {
      required: true
    },
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
      required: true
    }
  },
  data () {
    return {
      showModal: false
    }
  },
  watch: {
    show (val) {
      this.showModal = val
    }
  },
  methods: {
    onOk () {
      HttpRequestUtils.doPostWithFormParams(this.url, this.params, response => {
        if (!hasError(response)) {
          alert(this.message)
          this.$emit('success')
        }
      })
      this.$emit('show', false)
    },
    onCancel () {
      this.$emit('show', false)
    }
  }
}
</script>

<style scoped>

</style>
