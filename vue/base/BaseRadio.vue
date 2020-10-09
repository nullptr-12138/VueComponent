<template>
    <b-form-group :label="label" :label-for="id">
        <b-form-radio-group
            :id="id"
            v-model="sort"
            :options="options"
            >
        </b-form-radio-group>
    </b-form-group>
</template>

<script>
export default {
  name: 'item-sort-radio',
  model: {
    prop: 'value',
    event: 'input'
  },
  props: {
    value: {
      required: true
    },
    id: {
      type: String,
      default: 'sort-radio'
    },
    label: {
      type: String,
      default: '排序方式'
    },
    options: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      sort: ''
    }
  },
  watch: {
    sort (val) {
      if (val !== '') {
        this.$emit('input', val)
      } else {
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
