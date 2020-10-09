<script>
import BaseInput from '../../base/BaseInput'
export default {
  name: 'real-name-input',
  extends: BaseInput,
  props: {
    id: {
      type: String,
      default: 'real-name'
    },
    title: {
      type: String,
      default: '真实姓名'
    },
    required: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      validRegExp: /^[\u4e00-\u9fa5]{2,10}$/
    }
  },
  watch: {
    inputValue (val) {
      if (this.validRegExp.test(val)) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = '真实姓名输入不合法'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
