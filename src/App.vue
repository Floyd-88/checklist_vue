<template>
  <div class="checklist">
    <div class="checklist_main">
      <div class="checklist_header">
        <h1 class="checklist_header_title">Список дел на сегодня!!!</h1>
      </div>
      <div class="checklist_list">
        <ol class="checklist_list_ul" i-if="tasks">
          <li class="checklist_list_li" v-for="(elem, index) in tasks" :key="index">
            {{elem}}
          </li>
        </ol>
      </div>
      <div class="checklist_text">
      <textarea v-model="task" @keydown.enter.prevent.exact="addTask" class="checklist_text_textarea" placeholder="Сформировать задачу..."></textarea>
        <button @click="addTask" class="checklist_text_btn">Добавить задачу</button>
        <button @click="removeAllTasks" class="checklist_text_btn">Отчистить весь список</button>
      </div>
    </div>
  </div>


</template>

<script>


export default {
  data() {
    return {
      task: "",
      tasks: [],
    }
  },
  created() {
    let storage = localStorage.getItem("taskStorage");
    if(storage) {
     this.tasks = JSON.parse(storage)
    }
  },

  methods: {
    addTask: function () {
      this.tasks.push(this.task);
      localStorage.setItem("taskStorage", JSON.stringify(this.tasks))
      // localStorage.setItem(this.task, 'taskStorage')
      this.task = "";
    },

    removeAllTasks: function () {
      this.tasks = [];
      localStorage.removeItem('taskStorage')
    },

  }

}
</script>

<style>

</style>
