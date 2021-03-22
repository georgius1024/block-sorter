<template>
  <div class="row-wrapper">
    <draggable
      fallbackOnBody
      :group="draggingRow ? null : 'rows'"
      :swapThreshold="0.65"
      :value="row.cols"
      :sort="row.cols.length > 1"
      @input="$emit('input', $event)"
      @start="$emit('start')"
      @end="$emit('end')"
      class="row"
      ghostClass="col-ghost"
    >
      <Column v-for="(col, index) in row.cols" :key="index" class="col">
        {{ col }}
      </Column>
    </draggable>
  </div>
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
<style lang="scss" scoped>
.row-wrapper {
  display: flex;
  padding: 0px 16px;
  .row {
    flex-grow: 1;
    cursor: pointer;
    display: flex;
    flex-direction: row;
  }
}
.col-ghost {
  background: #00c5db;
  max-height: unset;
  height: auto;
  flex-grow: 1;
}
</style>