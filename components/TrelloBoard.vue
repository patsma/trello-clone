<template>
  <div>
    <div class="task" v-for="column in columns" :key="column.id">
      <div class="task__header">
        {{ column.title }}
      </div>
      <div class="task__title" v-for="task in column.tasks" :key="task.id">
        {{ task.title }}
      </div>
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
