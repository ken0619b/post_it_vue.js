<template>
  <div class="memo" :style="`left: ${left}px; top: ${top}px` "  >
    <div class="memo_wrapper">
      <div class="handle" @mousedown="sendDownEvent" @mouseup="sendUpEvent" @dragend="sendUpEvent" />
      <div class="delete_button" @click="clickDeleteButtonEvent">X</div>
    </div>
      <textarea class="text" />
  </div>
</template>

<script>
export default {
  props: ["left", "top", "memoId"],
  methods: {
    sendDownEvent(e) {
      //console.log("mousedown");
      this.$emit("mouseDown", {
        memoId: this.memoId
      });
    },
    sendUpEvent(e) {
      //console.log("mouseup");
      this.$emit("mouseUp", {
        memoId: this.memoId
      });
    },
    clickDeleteButtonEvent(e) {
      // console.log(
      //   `delete button has been clicked from memo id: ${this.memoId}`
      // );
      this.$emit("deleteButtonPressed", {
        memoId: this.memoId
      });
    }
  }
};
</script>
<style>
.memo {
  position: absolute;
  top: 20px;
  width: 200px;
  height: 300px;
  background-color: red;
}

.memo_wrapper {
  display: flex;
  height: 50px;
}

.text {
  width: 100%;
  height: 250px;
  background: transparent;
  color: #fff;
  font-size: 18px;
  border: none;
}

.delete_button {
  width: 10%;
  height: 50px;
  color: #fff;
  font-size: 30px;
  border: none;
}

.handle {
  width: 90%;
  height: 50px;
  background: rgba(0, 0, 0, 0.2);
}
</style>
