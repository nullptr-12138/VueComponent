<script>
import BaseInput from '../../base/BaseInput'

export default {
  name: 'id-card-input',
  extends: BaseInput,
  props: {
    id: {
      type: String,
      default: 'id-card'
    },
    title: {
      type: String,
      default: '身份证号码'
    },
    required: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      validRegExp: /(^\d{17}([0-9]|X|x)$)/
    }
  },
  watch: {
    inputValue (val) {
      if (this.validRegExp.test(val)) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = '身份证号码输入不合法'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
