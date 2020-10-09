<script>
import BaseInput from '../../base/BaseInput'

export default {
  name: 'age-input',
  extends: BaseInput,
  props: {
    id: {
      type: String,
      default: 'age'
    },
    title: {
      type: String,
      default: '年龄'
    },
    type: {
      type: String,
      default: 'number'
    }
  },
  watch: {
    inputValue (val) {
      if (val >= 15 && val <= 65) {
        this.description = ''
        this.$emit('input', val)
      } else {
        this.description = '年龄输入不合法'
        this.$emit('input', undefined)
      }
    }
  }
}
</script>

<style scoped>

</style>
