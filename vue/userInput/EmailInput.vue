<script>
import BaseInput from '../../base/BaseInput'

export default {
  name: 'email-input',
  extends: BaseInput,
  props: {
    id: {
      type: String,
      default: 'email'
    },
    title: {
      type: String,
      default: '电子邮箱'
    },
    required: {
      type: Boolean,
      default: true
    },
    type: {
      type: String,
      default: 'email',
      required: false
    }
  },
  data () {
    return {
      validRegExp: /^[A-Za-z0-9\u4e00-\u9fa5]+@[a-zA-Z0-9_-]+[.a-zA-Z0-9_-]*(\.((com)|(cn)))+$/
    }
  },
  watch: {
    inputValue (val) {
      if (this.validRegExp.test(val)) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = '邮箱输入不合法'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
