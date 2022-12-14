<template>
  <template v-if="statusChange">
    <ol class="checklist_list_ul" v-if="tasks">
      <li class="checklist_list_li" v-for="(elem, index) in tasks" :key="index">
          <span class="checklist_list_li_element"
                v-bind:class="{decoration_text: elem.isEdit}"
                @click="this.$emit('readyTask', $event)">
            {{ elem.name }}
          </span>
      </li>
    </ol>
  </template>
  <template v-else>
    <ol class="checklist_list_ul" v-if="tasks">
      <li class="checklist_list_li" v-for="(elem, index) in tasks" :key="index">
        <input type="text" v-model="elem.name">
      </li>
    </ol>
  </template>
</template>

<script>
export default {
  name: "BlockTasks",

  props: {
    tasks: {
      type: Array,
    },
    statusChange: {
      type: Boolean,
    },
  },
}
</script>

<style scoped>
.checklist_list_ul {

}

.checklist_list_li {
  font-size: 21px;
  margin: 7px;
  font-style: italic;
}

.checklist_list_li_element {
  cursor: pointer;
}

.decoration_text {
  text-decoration: line-through;
}
</style>