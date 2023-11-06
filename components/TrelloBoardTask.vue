<template>
  <div class="task bg-white p-4 m-4 rounded shadow-sm max-w-[250px]" :title="task.createdAt.toLocaleDateString()">
  <span>
    {{ task.title }}
  </span>
  </div>
</template>
<script lang="ts" setup>
import type {Task} from '@/types';

defineProps<{
  task: Task;
}>();
</script>
