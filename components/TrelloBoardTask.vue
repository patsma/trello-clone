<template>
  <div class="m-4 rounded bg-white p-4 shadow-sm task max-w-[250px]" :title="new Date(task.createdAt).toLocaleDateString()"
       @focus="focused = true"
       @blur="focused = false"
       tabindex="0"
  >
    <div class="grid grid-flow-col justify-start gap-1">
      <DragHandle/>
      <span class="pt-[2px]">
        {{ task.title }}
      </span>
    </div>
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
.task:focus,
.task:focus-visible{
  outline: lightgray auto 1px;
}
</style>
<script lang="ts" setup>
import type {Task, ID} from '@/types';
import DragHandle from "~/components/DragHandle.vue";

const props = defineProps<{
  task: Task;
}>();

const emit = defineEmits<{
  (e: "delete", payload: ID): void
}>();

const focused = ref(false);
onKeyStroke("Backspace", (e) => {
  if (focused.value) {
    emit("delete", props.task.id)
  }
});
</script>
