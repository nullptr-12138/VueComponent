<template>
    <b-form-group :label="label" :label-for="id">
        <b-form-select
                :id="id"
                class="form-control col-sm-4"
                v-model="select"
                :options="options"
                required
        >
        </b-form-select>
    </b-form-group>
</template>

<script>
import HttpRequestUtils from '../../assets/js/HttpRequestUtils'

export default {
  name: 'base-select',
  model: {
    prop: 'value',
    event: 'change'
  },
  props: {
    value: {
      required: true
    },
    id: {
      type: String,
      default: 'select'
    },
    label: {
      type: String,
      default: ''
    },
    url: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      select: '',
      options: []
    }
  },
  watch: {
    select (val) {
      this.$emit('change', val)
    }
  },
  mounted () {
    HttpRequestUtils.doGetWithoutParams(this.url, response => {
      this.options = response
      this.options.push('')
    })
  }
}
</script>

<style scoped>

</style>
