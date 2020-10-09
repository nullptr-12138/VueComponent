<template>
    <b-form-group
            :label="title"
            :label-for="id"
            :description="description"
    >
        <b-input-group class="mt-3">
            <b-input-group-prepend v-if="prepend">
                <slot name="prepend" ref="prepend"></slot>
            </b-input-group-prepend>
            <b-form-input
                v-model="inputValue"
                :id="id"
                :type="type"
                :required="required"
                :readonly="readonly"
                :placeholder="placeholder"
                trim
                v-if="area === false"
            >
            </b-form-input>
            <b-form-textarea
                    v-model="inputValue"
                    :id="id"
                    :rows="rows"
                    :max-rows="maxRows"
                    :placeholder="placeholder"
                    v-if="area === true"
            >
            </b-form-textarea>
            <b-input-group-append v-if="append">
                <slot name="append" ref="append"></slot>
            </b-input-group-append>
        </b-input-group>
    </b-form-group>
</template>

<script>
export default {
  name: 'base-input',
  model: {
    value: 'value',
    event: 'input'
  },
  props: {
    value: {
      required: true
    },
    id: {
      type: String,
      default: 'input'
    },
    title: {
      type: String,
      default: ''
    },
    area: {
      type: Boolean,
      default: false
    },
    type: {
      type: String,
      default: 'text'
    },
    rows: {
      type: Number,
      default: 3
    },
    maxRows: {
      type: Number,
      default: 6
    },
    placeholder: {
      type: String,
      default: ''
    },
    required: {
      type: Boolean,
      default: false
    },
    readonly: {
      type: Boolean,
      default: false
    },
    prepend: {
      type: Boolean,
      default: false
    },
    append: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      description: '',

      inputValue: this.value
    }
  },
  watch: {
    inputValue (val) {
      this.$emit('input', val)
    }
  },
  methods: {
    setDescription (description) {
      this.description = description
    }
  }
}
</script>

<style scoped>

</style>
