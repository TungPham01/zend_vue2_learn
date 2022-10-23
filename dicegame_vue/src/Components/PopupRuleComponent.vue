<template>
  <div class="wrapper_popup" :class="getClassPopup">
    <div class="rule">
      <h3>Luật chơi</h3>
      <p>Lorem ipsum dolor sit amet, consectet</p>
      <button class="confirm" @click="confirm">Đã hiểu</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "popup-rule",
  data() {
    return {

    }
  },
  props: {
    isOpenPopup: {
        type: Boolean,
        default: false
    }
  },
  methods: {
    confirm() {
        this.$emit('handleConfirm')
    }
  },
  computed: {
    getClassPopup: function () {
        return {
            'open-popup': this.isOpenPopup
        }
    }
  }
};
</script>

<style>
.wrapper_popup {
  position: fixed;
  top: 0;
  bottom: 0;
  right: 0;
  opacity: 0;
  visibility: hidden;
  left: 0;
  background-color: rgba(0, 0, 0, 0.4);
}
.wrapper_popup.open-popup {
    opacity: 1;
    visibility: visible;
}
.rule {
  width: 350px;
  padding: 10px;
  position: absolute;
  background-color: white;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.rule h3 {
  margin-bottom: 10px;
}
.rule button {
  margin-top: 10px;
}
.rule .confirm {
  border: 2px solid #333;
  padding: 5px;
  background-color: white;
  cursor: pointer;
}
</style>