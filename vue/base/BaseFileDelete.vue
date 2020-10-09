<template>
    <b-modal ok-title="是" cancel-title="否" centered hide-backdrop
             v-model="showModal" @ok="deleteFile" @cancel="onCancel">是否删除此文件</b-modal>
</template>

<script>
import HttpRequestUtils from '../../assets/js/HttpRequestUtils'
import {errorMessage} from '../../assets/js/ErrorMessage'

export default {
  name: 'base-file-delete',
  model: {
    prop: 'show',
    event: 'show'
  },
  props: {
    show: {
      type: Boolean,
      required: true
    },
    development: {
      type: Boolean,
      default: false
    },
    itemId: {
      required: true
    },
    fileId: {
      type: String,
      required: true
    }
  },
  computed: {
    url () {
      return this.development ? '/developer/item/file/delete' : '/user/item/file/delete'
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
    deleteFile () {
      const params = {id: this.itemId, file: this.fileId}
      HttpRequestUtils.doPostWithFormParams(this.url, params,
        response => errorMessage(response, '删除成功', true))
      this.$emit('show', false)
      this.$emit('delete')
    },
    onCancel () {
      this.$emit('show', false)
    }
  }
}
</script>

<style scoped>

</style>
