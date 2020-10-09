<template>
    <base-list :titleShow=true title="项目分类">
        <b-list-group-item v-for="(type, index) in types" :key="index">
            <b-badge>{{index + 1}}</b-badge>
            <base-router-link class="text-dark"
                url="ItemFindByType"
                :params="{type: type}"
            >
            {{ type }}</base-router-link>
        </b-list-group-item>
    </base-list>
</template>

<script>
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'
import BaseList from '../../base/BaseList'
import BaseLink from '../../base/BaseLink'
import BaseRouterLink from '../../base/BaseRouterLink'

export default {
  name: 'type-list',
  components: {BaseRouterLink, BaseLink, BaseList},
  data () {
    return {
      types: []
    }
  },
  mounted () {
    // 从接口获取数据
    HttpRequestUtils.doGetWithoutParams('/type/find', response => {
      this.types = response
    })
  }
}
</script>

<style scoped>
    ul > li {
        padding-left: 30%;
    }

</style>
