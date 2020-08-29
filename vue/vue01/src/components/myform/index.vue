<template>
  <div>
    <mForm :ruleForm="ruleForm" :rules="rules" ref="loginForm">
      <mFormItem label="用户名" prop="name">
        <minput v-model="ruleForm.name" type="text"></minput>
      </mFormItem>
      <mFormItem label="密码" prop="password">
        <minput v-model="ruleForm.password" type="password" name="password"></minput>
      </mFormItem>
      <mFormItem>
        <button @click="submit">提交</button>
      </mFormItem>
    </mForm>
    {{ruleForm}}
  </div>
</template>

<script>
  import minput from './minput.vue';
  import mFormItem from './mFormItem.vue';
  import mForm from './mForm.vue';
  export default {
    components: {
      minput,
      mFormItem,
      mForm,
    },
    data() {
      return {
        ruleForm: {
          name: '',
          password: ''
        },
        rules: {
          name: [{required: true, message: '用户名必填'}],
          password: [{required: true, message: '密码必填'}],
        }
      }
    },
    methods: {
      submit() {
        this.$refs.loginForm.validate((isValide) => {
          if(isValide) {
            alert('登录！！');
          }else {
            alert('错了！！');
          }
        });
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>