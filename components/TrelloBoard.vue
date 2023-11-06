<template>
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      class="flex items-start gap-8 overflow-x-auto p-4"
    >
      <template #item="{ element: column }: { element: Column }">
        <div class="column rounded bg-gray-200 p-4 task min-w-[250px]">
          <div class="p-4 font-bold task__header">
            {{ column.title }}
          </div>
          <TrelloBoardTask
            v-for="task in column.tasks"
            :key="task.id"
            :task="task"
          />
          <footer class="m-4 p-2">
            <button>+ Add Task</button>
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>

<script lang="ts" setup>
import type { Column } from "~/types";
import draggable from "vuedraggable";
import { nanoid } from "nanoid";

const columns = ref<Column[]>([
  {
    title: "Backlog",
    id: nanoid(),
    tasks: [
      {
        title: "Task 1",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Task 2",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Task 3",
        createdAt: new Date(),
        id: nanoid(),
      },
    ],
  },
  {
    title: "Selected for Dev",
    id: nanoid(),
    tasks: [],
  },
  {
    title: "Fix header",
    id: nanoid(),
    tasks: [],
  },
  {
    title: "In Progress",
    id: nanoid(),
    tasks: [],
  },
  {
    title: "Complete",
    id: nanoid(),
    tasks: [],
  },
]);
</script>
