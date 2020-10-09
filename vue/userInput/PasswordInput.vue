<script>
import BaseInput from '../../base/BaseInput'

export default {
  name: 'password-input',
  extends: BaseInput,
  props: {
    id: {
      type: String,
      default: 'password'
    },
    title: {
      type: String,
      default: '密码'
    },
    required: {
      type: Boolean,
      default: true
    },
    type: {
      type: String,
      default: 'password'
    }
  },
  watch: {
    inputValue (val) {
      if (val.length >= 6) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = '密码长度不足'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
