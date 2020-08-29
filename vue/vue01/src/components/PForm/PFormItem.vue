<template>
  <div>
    <label v-if="label">{{label}}</label>
    <slot></slot>
    <p v-if="errorMsg">{{errorMsg}}</p>
  </div>
</template>

<script>
  import Schema from 'async-validator';
  export default {
    inject: ['form'],
    props: {
      label: String,
      prop: String,
    },
    data() {
      return {
        errorMsg: ''
      }
    },
    mounted() {
      this.$on('validate', () => {
        this.validate();
      })
    },
    methods: {
      validate() {
        const rules = this.form.rules[this.prop];
        const value = this.form.loginForm[this.prop];

        const desc = {
          [this.prop]: rules
        }

        const validator = new Schema(desc);

        return validator.validate({[this.prop]: value}, (errors) => {
          if(errors) {
            console.log(123);
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