<template>
  <div>
    <div>
      <input type="text" v-model="newPhone" :focus="$emit('update:phone',newPhone)"/>
    </div>
  </div>
</template>

<script>
// 实现双向绑定
export default {
  name: "Login3",
  props: {
    phone: ""
  },
  data() {
    return {
      newPhone: this.phone
    };
  }
};
</script>

<style>
</style>
