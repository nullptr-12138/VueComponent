<script>
import BaseInput from '../../base/BaseInput'

export default {
  name: 'phone-input',
  extends: BaseInput,
  props: {
    id: {
      type: String,
      default: 'phone'
    },
    title: {
      type: String,
      default: '电话号码'
    }
  },
  data () {
    return {
      validRegExp: /^[1]\d{10}$/
    }
  },
  watch: {
    inputValue (val) {
      if (this.validRegExp.test(val)) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = '电话号码号码输入不合法'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
