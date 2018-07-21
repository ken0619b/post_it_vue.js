<template>
  <div class="container" @mousemove= "mouseMove" >
    <Memo v-for="mem in memoData" :key="mem.id" :memoId="mem.id" 
                                  :left='mem.left' :top='mem.top' 
                                  @mouseDown = "memoDown" @mouseUp = "memoUp"
                                  @deleteButtonPressed = "memoDelete" />
    <AddBtn @add="addMemo" />
  </div>
</template>

<script>
import Memo from "~/components/memo";
import AddBtn from "~/components/AddBtn";

export default {
  components: {
    Memo, //Memo: Memo
    AddBtn
  },
  //data: function()
  data() {
    return {
      memoData: [
        {
          id: 0,
          left: 20,
          top: 20,
          value: "aaaa",
          bgColor: "#f00",
          move: false
        }
      ],
      mousePotision: {
        x: null,
        y: null
      }
    };
  },
  methods: {
    addMemo(e) {
      //console.log(e);
      const memos = this.memoData.concat();
      let maxId = 0;
      for (let i = 0; i < memos.length; i++) {
        maxId = Math.max(maxId, memos[i].id);
      }
      memos.push({
        id: maxId + 1,
        left: memos[memos.length - 1].left + 220,
        top: 20,
        value: "aaaa",
        bgColor: "#f00",
        move: false
      });
      console.log(memos);
      this.memoData = memos;
    },
    memoDown(e) {
      console.log(`memo id:${e.memoId}'s move flag is true`);
      const memos = this.memoData.concat();

      memos.forEach((m, index) => {
        if (m.id == e.memoId) {
          memos[index].move = true;
          console.log(`m.id: ${m.id}'s flag has been changed to "true"`);
        }
      });

      // memos[0].move = true;
      this.memoData = memos;
      // console.log(this.memoData[0].left);
    },
    memoUp(e) {
      console.log(`memo id:${e.memoId}'s move flag is false`);
      const memos = this.memoData.concat();

      memos.forEach((m, index) => {
        if (m.id == e.memoId) {
          memos[index].move = false;
          console.log(`m.id: ${m.id}'s flag has been changed to "false"`);
        }
      });

      // memos[0].move = false;
      this.memoData = memos;
      // console.log(this.memoData[0].left);
    },
    mouseMove(e) {
      console.log(`memo id:${e.memoId}`);
      // console.log("gmousedown");
      // console.log(this.mousePotision);

      // initialize
      const currentX = e.clientX;
      const currentY = e.clientY;
      let originX = this.mousePotision.x;
      let originY = this.mousePotision.y;
      console.log(`clientX: ${originX} clientY: ${originY}`);
      console.log(`currentX: ${currentX} currentY: ${currentY}`);

      // check if mousePotision has already been initialized
      if (originX === null) {
        originX = currentX;
      }
      if (originY === null) {
        originY = currentY;
      }

      const diffX = currentX - originX;
      const diffY = currentY - originY;
      console.log(`diffX: ${diffX} diffY: ${diffY}`);

      const memos = this.memoData.concat();
      memos.forEach((m, index) => {
        if (m.move == true) {
          memos[index].left += diffX;
          memos[index].top += diffY;
          console.log(`m.id: ${m.id}'s potision has been changed`);
        }
      });

      this.memoData = memos;

      // if (this.memoData[0].move == true) {
      //   const memos = this.memoData.concat();
      //   memos[0].left += diffX;
      //   memos[0].top += diffY;
      //   this.memoData = memos;
      //   console.log(this.memoData[0].left);
      // }

      const newMousePosition = this.mousePotision;
      newMousePosition.x = currentX;
      newMousePosition.y = currentY;

      this.mousePotision = newMousePosition;

      console.log(this.mousePotision);
    },
    memoDelete(e) {
      console.log(` delete memo id:${e.memoId}`);

      const memos = this.memoData.concat();

      memos.forEach((m, index) => {
        if (m.id == e.memoId) {
          memos.splice(index, 1);
          console.log(`memo m.id: ${m.id} has been deleted`);
        }
      });

      this.memoData = memos;
    }
  }
};
</script>

<style scoped>
.container {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: center/cover url("~/assets/brick.jpg");
}
</style>
