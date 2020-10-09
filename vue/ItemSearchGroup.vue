<template>
    <b-form>
        <item-title-input v-model="condition.title" @search="onSearch"/>
        <base-select v-model="condition.type" id="type" label="类型选择" url="/type/find"/>
        <item-price-input v-model="condition.price"/>
        <item-time-input v-model="condition.time"/>
        <base-radio v-model="condition.sort" id="item-sort" label="排序方式" :options="options"/>
    </b-form>
</template>

<script>
import isValueValid from '../../../assets/js/ObjectVerificaiton'

import ItemTitleInput from './condition/ItemTitleInput'
import ItemPriceInput from './condition/ItemPriceInput'
import ItemTimeInput from './condition/ItemTimeInput'
import BaseRadio from '../../../components/base/BaseRadio'
import BaseSelect from '../../../components/base/BaseSelect'

export default {
  name: 'item-search-group',
  components: {BaseSelect, ItemTitleInput, ItemPriceInput, ItemTimeInput, BaseRadio},
  model: {
    prop: 'value',
    event: 'search'
  },
  props: {
    value: {
      required: true
    }
  },
  data () {
    return {
      condition: {
        title: undefined,
        type: undefined,
        price: {
          maxPrice: undefined,
          minPrice: undefined
        },
        time: undefined,
        sort: undefined
      },
      options: [
        { text: '价格', value: 'price' },
        { text: '时间', value: 'time' }
      ]
    }
  },
  methods: {
    getCondition () {
      let params = {}
      if (isValueValid(this.condition.title)) {
        params['title'] = this.condition.title
      }
      if (isValueValid(this.condition.type)) {
        params['type'] = this.condition.type
      }
      if (isValueValid(this.condition.price.minPrice)) {
        params['minPrice'] = this.condition.price.minPrice
        params['maxPrice'] = this.condition.price.maxPrice
      }
      if (isValueValid(this.condition.time)) {
        params['time'] = this.condition.time
      }
      if (isValueValid(this.condition.sort)) {
        params['sort'] = this.condition.sort
      }
      return params
    },
    onSearch () {
      const condition = this.getCondition()
      this.$emit('search', {...condition})
    }
  }
}
</script>

<style scoped>

</style>
