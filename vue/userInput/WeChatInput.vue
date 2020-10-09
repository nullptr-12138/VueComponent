<script>
import BaseInput from '../../base/BaseInput'

export default {
  name: 'weChat-input',
  extends: BaseInput,
  props: {
    id: {
      type: String,
      default: 'WeChat'
    },
    title: {
      type: String,
      default: '微信号码'
    }
  },
  data () {
    return {
      validRegExp: /^[a-zA-Z][-_a-zA-Z0-9]{1,19}/
    }
  },
  watch: {
    inputValue (val) {
      if (this.validRegExp.test(val)) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = '微信号码输入不合法'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
