<template>
  <textarea class="checklist_text_textarea" placeholder="Сформировать задачу..."
          :value="modelValue" @input="updateInput"
          @keydown.enter.prevent.exact="this.$emit('addTask')">
  </textarea>
</template>

<script>
export default {
  name: "BlockTextarea",

  props: {
    modelValue: [String, Number],
  },

  methods: {
    updateInput: function(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped>
.checklist_text_textarea {
  width: 340px;
  height: 70px;
}
</style>