<template>
    <div>
        <password-input ref="password" v-model="input" :title="inputName1"/>
        <password-strength
                :value="input"
                v-show="strengthShow"
        />
        <password-input
                id="repeat"
                :title="inputName2"
                ref="repeat"
                v-model="repeat"
        />
    </div>
</template>

<script>
import isValueValid from '../../../assets/js/ObjectVerificaiton'

import PasswordInput from './PasswordInput'
import PasswordStrength from '../PasswordStrength'

export default {
  name: 'password-input-group',
  components: {PasswordStrength, PasswordInput},
  model: {
    prop: 'password',
    event: 'input'
  },
  props: {
    password: {
      required: true
    },
    inputName1: {
      type: String,
      default: '密码'
    },
    inputName2: {
      type: String,
      default: '重复输入密码'
    }
  },
  data () {
    return {
      input: '',
      repeat: '',
      strengthShow: false
    }
  },
  watch: {
    input (val) {
      this.strengthShow = isValueValid(val) && val.length >= 6
    },
    repeat (val) {
      if (val !== this.input) {
        this.$refs.repeat.setDescription('密码输入不一致')
        this.$emit('input', undefined)
      } else {
        this.$refs.repeat.setDescription('')
        this.$emit('input', val)
      }
    }
  }
}
</script>

<style scoped>

</style>
