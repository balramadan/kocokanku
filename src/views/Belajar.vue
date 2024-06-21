<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <form @submit.prevent="addToList">
      <input type="text" v-model.lazy="names" />
      <input type="submit" value="Submit" />
    </form>
    <div class=""></div>
  </div>
</template>

<script>
export default {
  created() {},
  data() {
    return {
      state: true,
      inputName: '',
      names: [],
      error: '',
      showError: false
    }
  },
  props: {},
  methods: {
    addToList() {
      const userName = this.inputName

      if (this.validate(userName)) {
        this.names.push(userName)
        this.inputName = ''
        this.showError = false
      } else {
        this.showError = true
      }
    },
    
  }
}
</script>

<style lang="scss" scoped></style>
