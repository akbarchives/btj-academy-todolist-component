<script setup>
import { computed } from "vue";
import StatsList from "./components/StatsList.vue";
import FormAdd from "./components/FormAdd.vue";
import ListToDo from "./components/ListToDo.vue";
import ListDone from "./components/ListDone.vue";
</script>

<template>
  <div class="container mx-auto w-full p-8 lg:w-1/2">
    <h1 class="my-4 text-3xl font-bold">To Do App</h1>
    <StatsList />
    <FormAdd />
    <!-- To Do List -->
    <div class="container flex flex-col gap-4 sm:flex-row">
      <ListToDo />
      <ListDone />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: { name: "", priority: "" },
      toDoList: JSON.parse(localStorage.getItem("toDoList")) || [
        { name: "Belanja bahan masakan", priority: "High" },
        { name: "Rapat proyek", priority: "Medium" },
        { name: "Periksa email", priority: "Low" },
      ],
      toDoDone: JSON.parse(localStorage.getItem("toDoDone")) || [
        { name: "Buat laporan", priority: "High" },
        { name: "Olahraga", priority: "Low" },
      ],
    };
  },
  watch: {
    toDoList: {
      handler(newToDoList) {
        localStorage.setItem("toDoList", JSON.stringify(newToDoList));
      },
      deep: true,
    },
    toDoDone: {
      handler(newToDoDone) {
        localStorage.setItem("toDoDone", JSON.stringify(newToDoDone));
      },
      deep: true,
    },
  },
  computed: {
    countPending() {
      return this.toDoList.length;
    },
    countLowPriority() {
      return this.countPriority("Low");
    },
    countMediumPriority() {
      return this.countPriority("Medium");
    },
    countHighPriority() {
      return this.countPriority("High");
    },
    isToDoListEmpty() {
      if (this.toDoList.length === 0) {
        return true;
      }
    },
    isToDoDoneEmpty() {
      if (this.toDoDone.length === 0) {
        return true;
      }
    },
  },
  methods: {
    countPriority(priority) {
      let counts = 0;
      for (let i = 0; i < this.toDoList.length; i++) {
        if (this.toDoList[i].priority == priority) {
          counts += 1;
        }
      }
      return counts;
    },
    addToDoList() {
      if (this.newTodo.name && this.newTodo.priority) {
        this.toDoList.push({ ...this.newTodo });
        this.newTodo = { name: "", priority: "" }; // Clear input after adding
      }
    },
    deleteToDoList(index) {
      this.toDoList.splice(index, 1);
    },
    doneToDo(index) {
      const done = this.toDoList.splice(index, 1);
      this.toDoDone.push(done[0]);
    },
    deleteDone(index) {
      this.toDoDone.splice(index, 1);
    },
    unDone(index) {
      const undone = this.toDoDone.splice(index, 1);
      this.toDoList.push(undone[0]);
    },
    getPriorityClass(priority) {
      let low = false;
      let medium = false;
      let high = false;

      if (priority === "Low") {
        low = true;
      } else if (priority === "Medium") {
        medium = true;
      } else {
        high = true;
      }

      return {
        "bg-blue-400 ": low,
        "bg-orange-400 ": medium,
        "bg-red-400 ": high,
      };
    },
  },
  provide() {
    return {
      // data
      newTodo: this.newTodo,
      toDoList: this.toDoList,
      toDoDone: this.toDoDone,

      // method
      countPriority: this.countPriority,
      addToDoList: this.addToDoList,
      deleteToDoList: this.deleteToDoList,
      doneToDo: this.doneToDo,
      deleteDone: this.deleteDone,
      unDone: this.unDone,
      getPriorityClass: this.getPriorityClass,

      // computed
      countPending: computed(() => this.countPending),
      countLowPriority: computed(() => this.countLowPriority),
      countMediumPriority: computed(() => this.countMediumPriority),
      countHighPriority: computed(() => this.countHighPriority),
      isToDoListEmpty: computed(() => this.isToDoListEmpty),
    };
  },
};
</script>
