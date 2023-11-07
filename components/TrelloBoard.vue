<template>
  <div class="flex items-start gap-4 pb-24 overflow-x-auto">
    <draggable
        v-model="columns"
        group="columns"
        :animation="200"
        handle=".drag-handle"
        item-key="id"
        class="flex items-start gap-8 p-4"
    >
      <template #item="{ element: column }: { element: Column }">
        <div class="rounded bg-[#FFFFFF38] p-4 column task min-w-[250px]">
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
<style>
.column {
  background: rgba(255, 255, 255, 0.22);
}
</style>
<script lang="ts" setup>
import type {Column, Task} from "~/types";
import draggable from "vuedraggable";
import {nanoid} from "nanoid";
import DragHandle from "~/components/DragHandle.vue";

const columns = useLocalStorage<Column[]>("trelloBoard", [
  {
    title: "Bug Bounties",
    id: nanoid(),
    tasks: [
      {
        title: "Why did the div cross the road? To get to the other viewport.",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Fix the coffee machine (it's not coding errors, it's caffeine deficiency!)",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Investigate Schrödinger's bug - it only appears when not looking at the console.",
        createdAt: new Date(),
        id: nanoid(),
      },
    ],
  },
  {
    title: "To Debug",
    id: nanoid(),
    tasks: [
      {
        title: "Find the missing semicolon adventure.",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Play hide and seek with uncaught exceptions.",
        createdAt: new Date(),
        id: nanoid(),
      },
    ],
  },
  {
    title: "Refactoring Realm",
    id: nanoid(),
    tasks: [
      {
        title: "Rename variables from a1, a2... to something human-readable.",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Remove code commented out since the 'Before Times'.",
        createdAt: new Date(),
        id: nanoid(),
      },
    ],
  },
  {
    title: "In Progress",
    id: nanoid(),
    tasks: [
      {
        title: "Argue about tabs vs spaces - The Eternal Battle.",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Trying to center a div (Day 3).",
        createdAt: new Date(),
        id: nanoid(),
      },
    ],
  },
  {
    title: "Feature Factory",
    id: nanoid(),
    tasks: [
      {
        title: "Implement 'Dark Mode' because... well, we all love it!",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Add an easter egg that only activates when the Konami Code is entered.",
        createdAt: new Date(),
        id: nanoid(),
      },
    ],
  },
  {
    title: "Complete",
    id: nanoid(),
    tasks: [
      {
        title: "Successfully googled how to exit Vim.",
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: "Converted coffee into code - it's alive!",
        createdAt: new Date(),
        id: nanoid(),
      },
    ],
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
