<template>
        <base-input ref="emailCode" id="emailCode" title="邮箱验证码"
            v-model="code" :required=true :append=true>
            <b-button slot="append" variant="primary" @click="onSendEmail">发送验证码</b-button>
        </base-input>
</template>

<script>
import BaseInput from '../../base/BaseInput'
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'
import isValueValid from '../../../assets/js/ObjectVerificaiton'

export default {
  name: 'email-code-input',
  components: {BaseInput},
  model: {
    prop: 'value',
    event: 'input'
  },
  props: {
    value: {
      required: true
    },
    url: {
      type: String,
      default: ''
    },
    username: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      code: undefined
    }
  },
  watch: {
    code (val) {
      this.$emit('input', val)
    }
  },
  methods: {
    onSendEmail () {
      if (isValueValid(this.url)) {
        this.sendEmailByAddress()
      } else if (isValueValid(this.username)) {
        this.sendEmailByUsername()
      }
    },
    sendEmailByAddress () {
      const param = {
        email: this.url
      }
      HttpRequestUtils.doPostWithFormParams('/register/mailVerification', param,
        response => this.sendCallback(response))
    },
    sendEmailByUsername () {
      const param = {
        name: this.username
      }
      HttpRequestUtils.doPostWithFormParams('/user/password/mailVerification', param,
        response => this.sendCallback(response))
    },
    sendCallback (response) {
      if (response.hasOwnProperty('error')) {
        this.$refs.emailCode.setDescription(response.message)
      } else {
        this.$refs.emailCode.setDescription('发送成功')
      }
    }
  }
}
</script>

<style scoped>

</style>
