<template>
    <b-col>
        <b-table hover
                 ref="table"
                 id="items-table"
                 :fields="tableFields"
                 :per-page="size"
                 :items="items"
                 @row-hovered="getRowId">
            <template v-slot:cell(content)="data">
                <base-router-link
                    url="itemContent"
                    :params="{id: rowId, type: type}"
                >详细信息</base-router-link>
            </template>
            <template
                    v-slot:cell(owner)="data"
                    v-if="type !== 'owner'">
                <base-router-link
                    url="userFindByName"
                    :params="{name: data.item.owner, type: type}"
                >
                    {{data.item.owner}}
                </base-router-link>
            </template>
            <template
                    v-slot:cell(developer)="data"
                    v-if="type === 'owner' || type === 'admin'">
                <base-router-link
                        url="userFindByName"
                        :params="{name: data.item.developer, type: type}"
                   >
                    {{data.item.developer}}
                </base-router-link>
            </template>
            <template
                    v-slot:cell(contract)
                    v-if="type === 'common'">
                <b-link @click="showSubmitModal = true">承接</b-link>
                <base-modal v-model="showSubmitModal"
                    :params="{id: rowId}"
                    url="/developer/item/update/contract"
                    message="承接成功"
                    @success="$emit('contract')">
                            是否承接此项目
                </base-modal>
            </template>
            <template
                v-slot:cell(delete)
                v-if="type !== 'common'">
                <b-link @click="showDeleteModal = true">删除</b-link>
                <base-modal v-model="showDeleteModal"
                    :params="{id: rowId}" :url="urlPrefix + '/item/update/delete'"
                    message="删除成功"
                    @success="$emit('delete')">
                    是否删除此项目
                </base-modal>
            </template>
            <template
                    v-slot:cell(review)
                    v-if="type === 'owner'">
                <base-router-link :params="{id: rowId}" url="itemReview">审核</base-router-link>
            </template>
            <template
                    v-slot:cell(submit)
                    v-if="type === 'developer'">
                <b-link @click="showSubmitModal = true">提交</b-link>
                <base-modal v-model="showSubmitModal"
                            :params="{id: rowId}" url="/developer/item/update/submit"
                            message="提交成功">
                    是否提交此项目
                </base-modal>
            </template>
        </b-table>
        <b-pagination
                v-model="currentPage"
                :total-rows="rows"
                :per-page="size"
                aria-controls="items-table">
        </b-pagination>
    </b-col>
</template>

<script>
import BaseModal from '../../base/BaseModal'
import BaseRouterLink from '../../base/BaseRouterLink'

export default {
  name: 'item-table',
  components: {BaseRouterLink, BaseModal},
  model: {
    prop: 'value',
    event: 'change'
  },
  props: {
    value: {
      required: true
    },
    rows: {
      type: Number,
      default: 1
    },
    size: {
      type: Number,
      default: 20
    },
    items: {
      type: Array,
      required: true
    },
    type: {
      type: String,
      default: 'common',
      validator: function (value) {
        return ['common', 'owner', 'developer', 'admin'].indexOf(value) !== -1
      }
    }
  },
  computed: {
    tableFields () {
      let thead = [
        { key: 'id', label: '项目编号' },
        { key: 'title', label: '项目标题' },
        { key: 'type', label: '项目类型' },
        {key: 'owner', label: '项目发布者'},
        { key: 'time', label: '发布时间' },
        { key: 'price', label: '项目价格' }
      ]
      if (this.type !== 'common') {
        thead.push({key: 'status', label: '项目状态'})
        if (this.type === 'owner') {
          thead.push({key: 'developer', label: '项目承接者'})
          thead.splice(3, 1)
          thead.push({key: 'review', label: '审核'})
        } else if (this.type === 'developer') {
          thead.push({key: 'submit', label: '提交'})
        }
        thead.push({key: 'delete', label: '删除'})
      } else {
        thead.push({key: 'contract', label: '承接'})
      }
      thead.push({key: 'content', label: '详情信息'})
      console.log(thead)
      return thead
    },
    urlPrefix () {
      switch (this.type) {
        case 'owner': return '/user'
        case 'developer': return '/developer'
        case 'admin': return '/admin'
      }
    }
  },
  data () {
    return {
      currentPage: 1,
      rowId: undefined,
      showDeleteModal: false,
      showSubmitModal: false
    }
  },
  watch: {
    currentPage (val) {
      this.$emit('change', val)
    }
  },
  methods: {
    getRowId (item) {
      this.rowId = item.id
    },
    review () {
      this.$router.push({name: 'itemReview', params: this.rowId})
    }
  }
}
</script>

<style scoped>

</style>
