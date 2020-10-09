<script>
import BaseInput from '../../base/BaseInput'
import LoginCode from '../../common/LoginCode'

export default {
  name: 'login-code-input',
  extends: BaseInput,
  components: {LoginCode},
  props: {
    id: {
      type: String,
      default: 'loginCode'
    },
    title: {
      type: String,
      default: '验证码'
    }
  },
  data () {
    return {
      validRegExp: /^[a-zA-Z0-9]+$/
    }
  },
  watch: {
    inputValue (val) {
      if (val.length === 4 && this.validRegExp.test(val)) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = '验证码输入错误'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
