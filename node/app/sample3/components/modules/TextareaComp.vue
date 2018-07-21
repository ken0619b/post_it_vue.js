<template>
    <div>
      <p class="error">{{error}}</p>
        <textarea />
    </div>
</template>

<script>
export default {
  name: "textareaComp",
  data() {
    return {
      error: "入力必須"
    };
  }
};
</script>
<style>
.error {
  color: red;
}
</style>