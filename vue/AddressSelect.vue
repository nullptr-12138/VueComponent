<template>
    <b-form-group :label="name" :label-for="id">
        <b-form-select
                :id="id"
                class="form-control col-sm-4"
                v-model="value"
                :options="options"
                @change="doChange"
                required
        >
        </b-form-select>
        <address-select :parent-value="value" :options="childOptions"
        :count="count + 1" v-if="count < 3 && value !== null"
        @address-change="doAddressChange"/>
    </b-form-group>
</template>

<script>
import HttpRequestUtils from '../../assets/js/HttpRequestUtils'

export default {
  name: 'address-select',
  props: {
    parentValue: {
      type: String,
      required: false,
      default: null
    },
    count: {
      type: Number,
      required: false,
      default: 1
    },
    options: {
      type: Array,
      required: false,
      default: function () {
        if (this.count === 1) {
          let options = []
          HttpRequestUtils.doGetWithoutParams('/address/province', response => {
            for (let option of response) {
              const address = {
                value: option.proId,
                text: option.name
              }
              options.push(address)
            }
          })
          return options
        }
      }
    }
  },
  data () {
    return {
      value: null,
      childOptions: []
    }
  },
  computed: {
    id (val) {
      switch (this.count) {
        case 1: return 'province'
        case 2: return 'city'
        case 3: return 'county'
      }
    },
    name (val) {
      switch (this.count) {
        case 1: return '省'
        case 2: return '市'
        case 3: return '区'
      }
    }
  },
  methods: {
    doAddressChange (val) {
      this.$emit('address-change', val)
    },
    doChange () {
      switch (this.count) {
        case 1:
          this.setCities()
          break
        case 2:
          this.setCounties()
          break
        case 3:
          this.$emit('address-change', this.value)
      }
    },
    setCities () {
      let options = []
      const param = {
        id: this.value
      }
      HttpRequestUtils.doGetWithParams('/address/city', param, response => {
        for (let option of response) {
          const address = {
            value: option.cityId,
            text: option.name
          }
          options.push(address)
        }
      })
      this.childOptions = options
    },
    setCounties () {
      let options = []
      const param = {
        id: this.value
      }
      HttpRequestUtils.doGetWithParams('/address/county', param, response => {
        for (let option of response) {
          const address = {
            value: option.countyId,
            text: option.name
          }
          options.push(address)
        }
      })
      this.childOptions = options
    }
  }
}
</script>

<style scoped>

</style>
