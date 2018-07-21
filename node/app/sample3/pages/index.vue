<template>
  <div>
    Index
    <HeadComp></HeadComp>
    <TextareaComp></TextareaComp>
  </div>
</template>

<script>
import HeadComp from "@/components/modules/HeadComp";
import TextareaComp from "@/components/modules/TextareaComp";

export default {
  name: "form",
  components: {
    HeadComp,
    TextareaComp
  }
};
</script>

<style>
</style>
