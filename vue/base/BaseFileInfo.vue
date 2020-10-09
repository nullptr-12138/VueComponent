<template>
    <base-list :titleShow=true title="简历文件">
        <b-list-group-item v-for="(file, index) in files" :key="index">
            <span class="text-dark">名称: {{ file.name }}</span>
            <span class="text-dark">大小: {{ file.size }}</span>
            <span class="text-dark">上传时间: {{ file.time }}</span>
            <base-file-download :url="url" :fileId="file.id">下载</base-file-download>
            <div v-if="update">
                <b-link @click="showModal = true">删除</b-link>
                <base-file-delete v-model="showModal" @delete="deleteFile"
                  :development="development"  :item-id="itemId" :file-id="file.id"/>
            </div>
        </b-list-group-item>
    </base-list>
</template>

<script>
import BaseList from './BaseList'
import BaseFileDownload from './BaseFileDownload'
import BaseFileDelete from './BaseFileDelete'

export default {
  name: 'base-file-info',
  components: {BaseFileDelete, BaseList, BaseFileDownload},
  props: {
    files: {
      type: Array,
      required: true
    },
    update: {
      type: Boolean,
      required: true
    },
    development: {
      type: Boolean,
      required: false
    },
    itemId: {
      type: String,
      required: true
    },
    url: {
      type: String,
      default: '/file/download'
    }
  },
  data () {
    return {
      showModal: false
    }
  },
  methods: {
    deleteFile () {
      this.$emit('delete')
    }
  }
}
</script>

<style scoped>

</style>
