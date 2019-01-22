<template>
  <div>
    <div>
      <input type="text" v-model="newPhone">
    </div>
    <div>
      <input type="password" v-model="newPwd">
    </div>
  </div>
</template>

<script>
export default {
  name: "Login",
  props: {
    phone: "",
    pwd: ""
  },
  data() {
    return {
      newPhone: this.phone,
      newPwd: this.pwd
    };
  },
  watch: {
    phone(value) {
      this.newPhone = value;
    },
    newPhone(value) {
      this.$emit("on-chang-phone", value);
    }
  },
  methods: {
  }
};
</script>

<style>
</style>
