<template>
  <div class="w-full sm:w-1/2">
    <h1
      class="my-4 border border-transparent border-b-gray-200 py-2 text-3xl font-medium"
    >
      To Do
    </h1>
    <div
      v-if="!isToDoListEmpty"
      v-for="(list, index) in toDoList"
      :key="index"
      class="my-2 flex flex-col-reverse gap-2 rounded-lg border"
    >
      <div class="group flex flex-col gap-2 p-2 hover:bg-slate-100">
        <p class="text-2xl font-medium sm:text-base">{{ list.name }}</p>
        <div class="flex justify-between text-sm">
          <p class="flex items-center gap-1">
            <span
              class="inline-block h-3 w-3 rounded-sm"
              :class="getPriorityClass(list.priority)"
              >&nbsp;</span
            >
            {{ list.priority }}
          </p>
          <div class="flex gap-2">
            <button
              @click="deleteToDoList(index)"
              class="invisible rounded-md bg-red-500 px-2 py-1 font-medium text-white duration-200 ease-in-out hover:bg-red-600 group-hover:visible"
            >
              Delete
            </button>
            <button
              @click="doneToDo(index)"
              class="invisible rounded-md bg-green-500 px-2 py-1 font-medium text-white duration-200 ease-in-out hover:bg-green-600 group-hover:visible"
            >
              Done
            </button>
          </div>
        </div>
      </div>
    </div>
    <div
      v-else
      class="my-2 flex flex-col-reverse gap-2 rounded-lg px-2 py-6 text-center text-slate-500"
    >
      <p>Nothing to do</p>
    </div>
  </div>
</template>

<script>
export default {
  inject: [
    "isToDoListEmpty",
    "toDoList",
    "getPriorityClass",
    "deleteToDoList",
    "doneToDo",
  ],
};
</script>
