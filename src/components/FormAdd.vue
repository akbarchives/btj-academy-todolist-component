<template>
  <form
    @submit.prevent="addToDoList"
    class="flex flex-wrap items-end gap-2 rounded-lg border p-4 font-medium"
  >
    <div class="flex w-full flex-col sm:w-1/2">
      <label for="name">Todo's Name:</label>

      <input
        class="rounded-md border px-4 py-2"
        type="text"
        id="name"
        v-model="newTodo.name"
        required
        placeholder="What needs to be done?"
      />
    </div>
    <div class="flex grow flex-col">
      <label for="priority">Priority:</label>
      <select
        id="priority"
        v-model="newTodo.priority"
        required
        class="rounded-md border px-4 py-2"
      >
        <option value="" disabled>Select Priority</option>
        <option value="High">High</option>
        <option value="Medium">Medium</option>
        <option value="Low">Low</option>
      </select>
    </div>

    <button
      type="submit"
      class="h-1/2 w-full rounded-md bg-green-500 px-4 py-2 text-white hover:bg-green-600"
    >
      Add Todo
    </button>
  </form>
</template>

<script>
export default {
  inject: ["newTodo", "toDoList", "addToDoList"],
};
</script>
