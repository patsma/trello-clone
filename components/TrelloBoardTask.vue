<template>
  <div class="task bg-white p-4 m-4 rounded shadow-sm max-w-[250px]" :title="task.createdAt.toLocaleDateString()">
    <div class="grid grid-flow-col justify-start gap-1">
      <DragHandle/>
      <span class="pt-[2px]">
        {{ task.title }}
      </span></div>
  </div>
</template>
<script lang="ts" setup>
import type {Task} from '@/types';
import DragHandle from "~/components/DragHandle.vue";

defineProps<{
  task: Task;
}>();
</script>
