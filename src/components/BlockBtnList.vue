<template>
  <BlockBtn
      @click="this.$emit('addTask')"
      nameBtn="Добавить Задачу"
  />
  <BlockBtn
      @click="this.$emit('changeTasks')"
      :nameBtn="nameBtnChange"
  />
  <BlockBtn
      @click="this.$emit('removeAllTasks')"
      nameBtn="Очистить весь список"
  />
</template>

<script>
import BlockBtn from "@/components/BlockBtn";
export default {
  name: "BlockBtnList",
  components: {BlockBtn},
  props: {
    nameBtnChange: {
      type: String,
    }
  },
}
</script>

<style scoped>

</style>