<template>
  <div>
    <label v-if="label">
      {{label}}
    </label>
    <slot></slot>
    <p v-if="errorMsg">{{errorMsg}}</p>
  </div>
</template>

<script>
  import Schema from 'async-validator';
  export default {
    name: 'mFormItem',
    inject: ['form'],
    data() {
      return {
        errorMsg: ''
      }
    },
    props: {
      label: {
        type: String,
        default: ''
      },
      prop: String
    },
    mounted() {
      this.$on('validate', () => {
        this.validate();
      })
    },
    methods: {
      validate() {
        const ruleForm = this.form.ruleForm[this.prop];
        const rules = this.form.rules[this.prop];
        const desc = {
          [this.prop]: rules
        }
        const validator = new Schema(desc);
        return validator.validate({ [this.prop]: ruleForm }, (errors, fields) => {
          if(errors) {
            this.errorMsg = errors[0].message;
          }else {
            this.errorMsg = '';
          }
        })
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>