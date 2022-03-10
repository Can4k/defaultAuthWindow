<template>
  <img
      @click="close"
      class="close-button"
      src="@/components/authWindow/assets/x-circle.svg"
      alt="закрыть"
  >
</template>

<script>
export default {
  name: "closeButton",
  methods: {
    close() {
      this.$emit("closeClicked");
    }
  }
}
</script>

<style scoped>
.close-button {
  position: absolute;
  width: 24px;
  right: 8px;
  cursor: pointer;
}
.close-button:hover {
  transform: scale(1.04);
}
</style>