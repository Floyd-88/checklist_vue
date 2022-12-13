<template>
  <div class="checklist">
    <div class="checklist_main">
      <div class="checklist_header">
        <h1 class="checklist_header_title">Список дел на сегодня!!!</h1>
      </div>
      <div class="checklist_list">
        <template v-if="statusChange">
          <ol class="checklist_list_ul" i-if="tasks">
            <li class="checklist_list_li" v-for="(elem, index) in tasks" :key="index">
              <span class="checklist_list_li_element"  v-bind:class="{decoration_text: elem.isEdit}" @click="readyTask($event)">{{elem.name}}</span>
            </li>
          </ol>
        </template>
        <template v-else>
          <ol class="checklist_list_ul" i-if="tasks">
            <li class="checklist_list_li" v-for="(elem, index) in tasks" :key="index">
              <input type="text" v-model="elem.name">
            </li>
          </ol>
        </template>
      </div>
      <div class="checklist_text">
      <textarea v-model="task" @keydown.enter.prevent.exact="addTask" class="checklist_text_textarea" placeholder="Сформировать задачу..."></textarea>
        <button @click="addTask" class="checklist_text_btn">Добавить задачу</button>
        <button class="checklist_text_btn" @click="changeTasks">{{nameBtnChange}}</button>
        <button @click="removeAllTasks" class="checklist_text_btn">Очистить весь список</button>
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
      statusChange: true,
      nameBtnChange: "Редактировать список",
    }
  },

  mounted() {
    let storage = localStorage.getItem("taskStorage");
    if(storage) {
      this.tasks = JSON.parse(storage);
    }
    },

  methods: {
    addTask: function () {
      if(this.task) {
        this.tasks.push({
          name: this.addEndStr(this.task),
          isEdit: false,
        });
        localStorage.setItem("taskStorage", JSON.stringify(this.tasks))
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

    addEndStr: function(str) {
      str = str.trim();
      if(str.substr(str.length -1) !== "!") {
       str = str.replace(/[.;:]$/g, '') + '!';
      }
      return str;
    },

    changeTasks: function() {
      this.statusChange = !this.statusChange;
      (this.statusChange) ? this.nameBtnChange = "Редактировать список" : this.nameBtnChange = "Cохранить изменения";
      for(let elem of this.tasks) {
        if(elem.name) {
          elem.name = this.addEndStr(elem.name)
        } else {
          this.tasks = this.tasks.filter(i => i.name !== "")
        }
      }
      localStorage.setItem("taskStorage", JSON.stringify(this.tasks))
    }
  },

}
</script>

<style>
</style>
