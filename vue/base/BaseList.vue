<template>
  <b-list-group>
    <b-list-group-item v-if="titleShow">
      <span class="text-dark">{{title}}</span>
    </b-list-group-item>
    <slot></slot>
  </b-list-group>
</template>

<script>
export default {
  name: 'base-list',
  props: {
    titleShow: {
      type: Boolean,
      default: true
    },
    title: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped></style>
