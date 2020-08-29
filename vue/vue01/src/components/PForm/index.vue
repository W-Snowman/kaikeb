<template>
  <div>
    <p-formm :rules="rules" :loginForm="loginForm" ref="pform">
      <p-form-item label="用户名" prop="name">
        <p-input v-model="loginForm.name" type="text"></p-input>
      </p-form-item>
      <p-form-item label="密码" prop="password">
        <p-input v-model="loginForm.password" type="password"></p-input>
      </p-form-item>
      <p-form-item>
        <button @click="validate">登录</button>
      </p-form-item>
    </p-formm>

    {{loginForm}}
  </div>
</template>

<script>
  import PInput from '@/components/PForm/PInput.vue';
  import PFormItem from '@/components/PForm/PFormItem.vue';
  import PFormm from '@/components/PForm/PFormm.vue';
  export default {
    components: {
      PInput,
      PFormItem,
      PFormm,
    },
    data() {
      return {
        loginForm: {
          name: '',
          password: ''
        },
        rules: {
          name: [{required: true, message: '用户名必填'}],
          password: [{required: true, message: '密码必填'}]
        }
      }
    },
    methods: {
      validate() {
        this.$refs.pform.validate( (isValide) => {
          if(isValide) {
            alert("登录！！");
          }else {
            alert("错了！！");
          }
        });
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>