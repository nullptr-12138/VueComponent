<template>
    <b-link id="download" @click="download">
        <slot></slot>
    </b-link>
</template>

<script>
import HttpRequestUtils from '../../assets/js/HttpRequestUtils'
import {hasError} from '../../assets/js/ErrorMessage'

export default {
  name: 'base-file-download',
  props: {
    url: {
      type: String,
      required: true
    },
    fileId: {
      type: String,
      required: true
    }
  },
  methods: {
    download () {
      const param = {
        id: this.fileId
      }
      HttpRequestUtils.fileDownload(this.url, param, response => {
        if (!hasError(response)) {
          let link = document.createElement('a')
          if ('download' in link) {
            // 设置下载文件名称
            link.download = response.name
            // 设置下载内容链接
            link.href = URL.createObjectURL(response.bytes)
            link.click()
            URL.revokeObjectURL(link.href)
            document.removeChild(link)
            // IE10+下载
          } else {
            navigator.msSaveBlob(response.bytes, response.name)
          }
        }
      })
    }
  }
}
</script>

<style scoped>

</style>
