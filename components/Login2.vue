<template>
  <div>
    <div>
      <input type="text" v-model="newPhone"/>
    </div>
    <div>
      <input type="password" v-model="newPwd" :focus="$emit('input', newPwd)"/>
    </div>
  </div>
</template>

<script>
// 实现双向绑定
export default {
  name: "Login2",
  props: {
    value: "",
    phone: ""
  },
  data() {
    return {
      newPhone: this.phone,
      newPwd: this.value
    };
  },
  watch: {
    phone(value) {
      this.newPhone = value;
    },
    newPhone(value) {
      this.$emit("on-chang-phone", value);
    }
  }
};
</script>

<style>
</style>
