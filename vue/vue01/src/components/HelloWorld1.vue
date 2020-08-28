<template>
  <div>
    <div>{{ msg1 }}</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld1',
  data () {
    return {
      msg1: '花见花开还看见'
    }
  },
  created() {
    this.$parent.$on('mua', (e) => {
      console.log(e);
    });

    this.$bus.$on('transData', (e) => {
      console.log(e);
    })
  }
}
</script>
