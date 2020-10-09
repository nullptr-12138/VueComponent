<template>
    <b-form>
        <b-form-file
                :state="Boolean(this.files)"
                placeholder="选择一个文件或拖拽至此"
                drop-placeholder="拖拽文件至此"
                v-model="files" :multiple="!single">
            <template slot="file-name" slot-scope="{names}">
                <b-badge variant="dark" v-for="(name, index) in names" :key="index">{{name}}</b-badge>
            </template>
        </b-form-file>
        <b-button @click="uploadFiles">提交</b-button>
    </b-form>
</template>

<script>
import HttpRequestUtils from '../../assets/js/HttpRequestUtils'
import {hasError} from '../../assets/js/ErrorMessage'

export default {
  name: 'base-upload-file',
  props: {
    itemId: {
      type: String,
      default: ''
    },
    developmentFile: {
      type: Boolean,
      default: false
    },
    single: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    url () {
      if (this.single) {
        return '/developer/update/upload'
      } else {
        return this.developmentFile ? '/developer/item/file/upload' : '/user/item/file/upload'
      }
    }
  },
  data () {
    return {
      files: undefined
    }
  },
  methods: {
    uploadFiles () {
      if (this.files.length !== 0) {
        let params = new FormData()
        params.append('id', this.itemId)
        if (this.single) {
          params.append('resume', this.files)
        } else {
          for (let file of this.files) {
            params.append('files', file)
          }
        }
        HttpRequestUtils.fileUpload(this.url, params, response => {
          if (!hasError(response)) {
            this.$emit('upload')
          }
        })
      } else {
        alert('没有选择上传文件')
      }
    }
  }
}
</script>

<style scoped>

</style>
