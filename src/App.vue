<template>
  <div class="checklist">
    <div class="checklist_main">
      <div class="checklist_header">
        <h1 class="checklist_header_title">Список дел на сегодня!!!</h1>
      </div>
      <div class="checklist_list">
        <ol class="checklist_list_ul" i-if="tasks">
          <li class="checklist_list_li" v-for="(elem, index) in tasks" :key="index">
            <span class="checklist_list_li_element"  @click="readyTask($event)">{{elem.name}}</span>
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

  mounted() {
    let storage = localStorage.getItem("taskStorage");
    if(storage) {
      this.tasks = JSON.parse(storage);
    }
    this.$nextTick(function () {
        this.mountedReady()
    })
    },

  methods: {
    addTask: function () {
      if(this.task) {
        this.tasks.push({
          name:this.task,
          isEdit: false,
        });
        localStorage.setItem("taskStorage", JSON.stringify(this.tasks))
        // localStorage.setItem(this.task, 'taskStorage')
        this.task = "";
      }
    },

    removeAllTasks: function () {
      this.tasks = [];
      localStorage.removeItem('taskStorage')
    },

    readyTask: function(e) {
      let element_task = e.target;
     element_task.classList.toggle("decoration_text")
      this.tasks = this.tasks.map((task) => {
        if(task.name === element_task.innerHTML) {
          task.isEdit = !task.isEdit;
        }
        return task;
      })
      localStorage.setItem("taskStorage", JSON.stringify(this.tasks))
    },

    mountedReady: function() {
      let checklist_list_ul = document.querySelectorAll(".checklist_list_li_element")
      for(let task of this.tasks) {
        if(task.isEdit) {
          for(let elem of checklist_list_ul) {
            if(elem.innerHTML === task.name)
              elem.classList.add("decoration_text")
          }
        }
      }
    }
  }

}
</script>

<style>
</style>
