<template>
  <div class="ref-component">
    <h1>Ref</h1>
    <button @click="handleClick">Chọn file</button>
    <input ref="fileInput" type="file" style="display: none">
  </div>
</template>

<script>
export default {
  name: "ref-component",
  data() {
    return {};
  },
  methods: {
    handleClick () {
        this.$refs.fileInput.click()
    }
  }
};
</script>

<style>
</style>