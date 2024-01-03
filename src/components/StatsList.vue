<template>
  <!-- Report -->
  <div class="flex flex-wrap gap-4 py-5 text-center">
    <div
      class="h-20 w-20 rounded-md border bg-slate-200 p-2 transition hover:bg-slate-300"
    >
      <p class="font-medium">Pending</p>
      <p class="text-2xl font-bold">{{ countPending }}</p>
    </div>
    <div
      class="h-20 w-20 rounded-md border bg-blue-200 p-2 transition hover:bg-blue-300"
    >
      <p class="font-medium">Low</p>
      <p class="text-2xl font-bold">{{ countLowPriority }}</p>
    </div>
    <div
      class="h-20 w-20 rounded-md border bg-orange-200 p-2 transition hover:bg-orange-300"
    >
      <p class="font-medium">Medium</p>
      <p class="text-2xl font-bold">{{ countMediumPriority }}</p>
    </div>
    <div
      class="h-20 w-20 rounded-md border bg-red-200 p-2 transition hover:bg-red-300"
    >
      <p class="font-medium">High</p>
      <p class="text-2xl font-bold">{{ countHighPriority }}</p>
    </div>
  </div>
</template>

<script>
export default {
  inject: [
    "countPending",
    "countLowPriority",
    "countMediumPriority",
    "countHighPriority",
  ],
};
</script>
