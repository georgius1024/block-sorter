<template>
  <draggable
    fallbackOnBody
    :group="draggingRow ? null : 'rows'"
    :swapThreshold="0.65"
    :value="row.cols"
    :sort="row.cols.length > 1"
    @input="$emit('input', $event)"
    class="row"
    ghostClass="col-ghost"
  >
    <Column v-for="(col, index) in row.cols" :key="index" class="col">
      {{ col }}
    </Column>
  </draggable>
</template>
<script>
import draggable from "vuedraggable";
import Column from "./Column";

export default {
  name: "Row",
  components: {
    Column,
    draggable,
  },
  props: {
    row: {
      type: Object,
    },
    draggingRow: {
      type: Boolean,
    },
  },
};
</script>
<style scoped>
.row {
  cursor: pointer;
  display: flex;
  flex-direction: row;
  padding: 12px 16px;
}
.col-ghost {
  background: #00c5db;
  max-height: unset;
  height: auto;
  flex-grow: 1;
}
</style>