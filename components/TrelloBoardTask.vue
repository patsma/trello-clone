<template>
  <div class="task bg-white p-4 m-4 rounded shadow-sm max-w-[250px]" :title="task.createdAt.toLocaleDateString()">
    <div class="grid grid-flow-col justify-start gap-1">
      <DragHandle/>
      <span class="pt-[2px]">
        {{ task.title }}
      </span></div>
  </div>
</template>
<style>


.sortable-chosen {
}

.sortable-drag .task {
  transform: rotate(6deg);
}

.sortable-ghost .task {
  position: relative;
}

.sortable-ghost .task::after {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  background: rgba(128, 128, 128, 0.88);
  border-radius: 1rem;
}
</style>
<script lang="ts" setup>
import type {Task} from '@/types';
import DragHandle from "~/components/DragHandle.vue";

defineProps<{
  task: Task;
}>();
</script>
