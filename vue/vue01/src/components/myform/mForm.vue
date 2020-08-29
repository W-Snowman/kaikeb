<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: 'mForm',
    provide() {
      return {
        form: this
      }
    },
    props: {
      ruleForm: {
        type: Object,
        required: true
      },
      rules: {
        type: Object
      }
    },
    methods: {
      validate(callback) {
        const tasks = this.$children
          .filter((item) => item.prop)
          .map((item) => item.validate());
        Promise.all(tasks)
          .then(() => callback(true))
          .catch(() => callback(false));
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>