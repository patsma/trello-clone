<template>
  <div class="flex items-start gap-4 overflow-x-auto">
    <draggable
        v-model="columns"
        group="columns"
        :animation="200"
        handle=".drag-handle"
        item-key="id"
        class="flex items-start gap-8 p-4"
    >
      <template #item="{ element: column }: { element: Column }">
        <div class="rounded bg-gray-200 p-4 column task min-w-[250px]">
          <div
              class="grid grid-flow-col items-center justify-start gap-2 p-4 font-bold task__header align-center"
          >
            <DragHandle/>
            <input
                class="title-input w-4/5 rounded bg-transparent px-1 focus:bg-white mt-1"
                v-model="column.title"
                @keyup.enter="($event.target as HTMLInputElement).blur()"
                @keydown.backspace="column.title ==='' ? (columns = columns.filter(c => c.id !== column.id)) : null"
                type="text">
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
                    @delete="column.tasks = column.tasks.filter(t => t.id !== task.id)"
                />
              </div>
            </template>
          </draggable>
          <footer class="p-2">
            <NewTask @add="column.tasks.push($event)"/>
          </footer>
        </div>
      </template>
    </draggable>
    <button
        @click="createColumn"
        class="whitespace-nowrap rounded bg-gray-200 p-4 mt-4 opacity-50"
    >
      + Add Column
    </button>
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

function createColumn() {
  const column: Column = {
    title: "",
    id: nanoid(),
    tasks: [],
  };
  columns.value.push(column);
  nextTick(() => {

    (document.querySelector('.column:last-of-type .title-input') as HTMLInputElement).focus();

  })
}
</script>
