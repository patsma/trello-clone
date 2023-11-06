<template>
  <div class="flex gap-8 overflow-x-auto items-start p-4">
    <div class="task bg-gray-200 p-4 rounded min-w-[250px]" v-for="column in columns" :key="column.id">
      <div class="task__header p-4 font-bold">
        {{ column.title }}
      </div>
      <TrelloBoardTask v-for="task in column.tasks" :key="task.id" :task="task"/>
      <footer class="p-2 m-4">
        <button>
          + Add Task
        </button>
      </footer>
    </div>
  </div>
</template>
<script lang="ts" setup>
import type {Column} from '~/types';
import {nanoid} from 'nanoid';

const columns = ref<Column[]>([
  {
    title: 'Backlog',
    id: nanoid(),
    tasks: [
      {
        title: 'Task 1',
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: 'Task 2',
        createdAt: new Date(),
        id: nanoid(),
      },
      {
        title: 'Task 3',
        createdAt: new Date(),
        id: nanoid(),
      },
    ],
  },
  {
    title: 'Selected for Dev',
    id: nanoid(),
    tasks: [],
  },
  {
    title: 'Fix header',
    id: nanoid(),
    tasks: [],
  },
  {
    title: 'In Progress',
    id: nanoid(),
    tasks: [],
  },
  {
    title: 'Complete',
    id: nanoid(),
    tasks: [],
  },

])
</script>
