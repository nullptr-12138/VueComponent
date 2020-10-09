<script>
import BaseInput from '../../base/BaseInput'

export default {
  name: 'qq-input',
  extends: BaseInput,
  props: {
    id: {
      type: String,
      default: 'qq'
    },
    title: {
      type: String,
      default: 'QQ号码'
    }
  },
  data () {
    return {
      validRegExp: /^[1-9][0-9]{1,10}/
    }
  },
  watch: {
    inputValue (val) {
      if (this.validRegExp.test(val)) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = 'QQ号码输入不合法'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
