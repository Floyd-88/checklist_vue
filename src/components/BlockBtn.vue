<template>
  <button class="checklist_text_btn">{{nameBtn}}</button>
</template>

<script>
export default {
  name: "BlockBtn",

  props: {
    nameBtn: {
      type: String,
    }
  }
}
</script>

<style scoped>
.checklist_text_btn {
  margin: 7px;
  background: cornsilk;
  border: 1px solid cadetblue;
  padding: 6px;
  box-shadow: 1px 0px 2px 1px rgb(0 0 0 / 50%);
  font-size: 15px;
  cursor: pointer;
}
.checklist_text_btn:hover {
  background: #dbd1a6;
  transition: .3s;
}
</style>