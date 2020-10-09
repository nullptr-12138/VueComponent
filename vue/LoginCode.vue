<template>
    <b-img @click="getCode" :src="image" fluid alt="Responsive image"></b-img>
</template>

<script>
import HttpRequestUtils from '../../assets/js/HttpRequestUtils'

export default {
  name: 'login-code',
  data () {
    return {
      image: ''
    }
  },
  methods: {
    getCode () {
      HttpRequestUtils.getVerificationCode(image => { this.image = image })
    }
  },
  mounted () {
    this.getCode()
  }
}
</script>

<style scoped>

</style>
