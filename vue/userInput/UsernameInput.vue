<script>
import InfoInput from '../../base/BaseInput'

export default {
  name: 'username-input',
  extends: InfoInput,
  props: {
    id: {
      type: String,
      default: 'username'
    },
    title: {
      type: String,
      default: '用户名'
    },
    required: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      validRegExp: /^[a-zA-Z0-9_\u4e00-\u9fa5]+$/
    }
  },
  watch: {
    inputValue (value) {
      if (value.length <= 15 && this.validRegExp.test(value)) {
        this.description = ''
        this.$emit('input', value)
      } else {
        this.description = '用户名输入不合法'
        this.$emit('input', undefined)
      }
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
