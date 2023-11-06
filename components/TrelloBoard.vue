<template>
  <div>
    <draggable
        v-model="columns"
        group="columns"
        :animation="200"
        handle=".drag-handle"
        item-key="id"
        class="flex items-start gap-8 overflow-x-auto p-4"
    >
      <template #item="{ element: column }: { element: Column }">
        <div class="rounded bg-gray-200 p-4 column task min-w-[250px]">
          <div
              class="grid grid-flow-col items-center justify-start gap-2 p-4 font-bold task__header align-center"
          >
            <DragHandle/>
            <div class="grid pt-1">{{ column.title }}</div>
          </div>

          <draggable
              v-model="column.tasks"
              :group="{ name: 'tasks', pull: alt ? 'clone' : true}"
              :animation="200"
              handle=".drag-handle"
              item-key="id"
          >
            <template #item="{element:task}:{element:Task}">
              <div class="task">
                <TrelloBoardTask
                    :task="task"
                />
              </div>
            </template>
          </draggable>

          <footer class="m-4 p-2">
            <button>+ Add Task</button>
          </footer>
        </div>
      </template>
    </draggable>
  </div>
</template>
<script lang="ts" setup>
import type {Column, Task} from "~/types";
import draggable from "vuedraggable";
import {nanoid} from "nanoid";
import DragHandle from "~/components/DragHandle.vue";
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
const alt = useKeyModifier("Alt")
</script>
