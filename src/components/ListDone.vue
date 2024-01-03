<template>
  <div class="w-full sm:w-1/2">
    <h1
      class="my-4 border border-transparent border-b-gray-200 py-2 text-3xl font-medium"
    >
      Done
    </h1>
    <div
      v-if="!isToDoDoneEmpty"
      v-for="(list, index) in toDoDone"
      :key="index"
      class="my-2 flex flex-col gap-2 rounded-lg border"
    >
      <div class="group flex flex-col gap-2 p-2 hover:bg-slate-50">
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
              @click="deleteDone(index)"
              class="invisible rounded-md bg-red-500 px-2 py-1 font-medium text-white duration-200 ease-in-out hover:bg-red-600 group-hover:visible"
            >
              Delete
            </button>
            <button
              @click="unDone(index)"
              class="invisible rounded-md bg-green-500 px-2 py-1 font-medium text-white duration-200 ease-in-out hover:bg-green-600 group-hover:visible"
            >
              Undone
            </button>
          </div>
        </div>
      </div>
    </div>
    <div
      v-else-if="isToDoListEmpty && isToDoDoneEmpty"
      class="my-2 flex flex-col-reverse gap-2 rounded-lg px-2 py-6 text-center text-slate-500"
    >
      <p>Get some rest</p>
    </div>
    <div
      v-else
      class="my-2 flex flex-col-reverse gap-2 rounded-lg px-2 py-6 text-center text-slate-500"
    >
      <p>Let's do it</p>
    </div>
  </div>
</template>

<script>
export default {
  inject: [
    "isToDoDoneEmpty",
    "toDoDone",
    "getPriorityClass",
    "deleteDone",
    "unDone",
  ],
};
</script>
