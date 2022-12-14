<template>
  <div class="checklist">
    <div class="checklist_main">
      <div class="checklist_header">
        <h1 class="checklist_header_title">Список дел на сегодня!!!</h1>
      </div>
      <div class="checklist_list">
        <BlockTasks
            :tasks="tasks"
            :statusChange="statusChange"
            @readyTask="readyTask"
        />
      </div>
      <div class="checklist_text">
        <BlockTextarea
            v-model="task"
            @addTask="addTask"
        />
        <BlockBtnList
            :nameBtnChange="nameBtnChange"
            @addTask="addTask"
            @changeTasks="changeTasks"
            @removeAllTasks="removeAllTasks"
        />
      </div>

    </div>
  </div>
</template>

<script>
import BlockTasks from "@/components/BlockTasks";
import BlockTextarea from "@/components/BlockTextarea";
import BlockBtnList from "@/components/BlockBtnList";

export default {
  components: {BlockBtnList, BlockTextarea, BlockTasks},
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
    if (storage) {
      this.tasks = JSON.parse(storage);
    }
  },

  methods: {
    addTask: function () {
      if (this.task) {
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

    readyTask: function (e) {
      let element_task = e.target;
      element_task.classList.toggle("decoration_text")
      this.tasks = this.tasks.map((task) => {
        if (task.name === element_task.innerHTML) {
          task.isEdit = !task.isEdit;
        }
        return task;
      })
      localStorage.setItem("taskStorage", JSON.stringify(this.tasks))
    },

    addEndStr: function (str) {
      str = str.trim();
      if (str.substr(str.length - 1) !== "!") {
        str = str.replace(/[.;:]$/g, '') + '!';
      }
      return str;
    },

    changeTasks: function () {
      this.statusChange = !this.statusChange;
      (this.statusChange) ? this.nameBtnChange = "Редактировать список" : this.nameBtnChange = "Cохранить изменения";
      for (let elem of this.tasks) {
        if (elem.name) {
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
