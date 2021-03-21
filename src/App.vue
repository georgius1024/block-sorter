<template>
  <div id="app">
    <draggable
      fallbackOnBody
      class="rows"
      group="rows"
      ghostClass="row-ghost"
      :swapThreshold="0.65"
      :value="rows"
      @input="input"
      @start="draggingRow = true"
      @end="draggingRow = false"
    >
      <!-- <div style="padding: 1px 16px"></div> -->

      <Row
        v-for="row in rows"
        :row="row"
        :draggingRow="draggingRow"
        @input="inputRow(row.id, $event)"
        :key="row.id"
      />
    </draggable>
  </div>
</template>

<script>
// TODO LIMIT 3 BLOCKS/ROW
import draggable from "vuedraggable";
import Row from "./components/Row";

export default {
  name: "App",
  components: {
    draggable,
    Row,
  },
  data() {
    return {
      draggingRow: false,
      draggingCol: false,
      id: 10,
      rows: [
        { id: 1, cols: [1, 2, 3] },
        { id: 2, cols: [4, 5, 6] },
        { id: 3, cols: [7, 8, 9] },
      ],
    };
  },
  methods: {
    input(value) {
      const rows = [...value]
        .map((e) =>
          e.id && Array.isArray(e.cols) ? e : { id: this.id++, cols: [e] }
        )
        .filter((e) => e.cols.length);
      this.$set(this, "rows", rows);
    },
    inputRow(id, cols) {
      this.$nextTick().then(() => {
        const rows = [...this.rows]
          .map((e) => (e.id === id ? { id, cols } : e))
          .filter((e) => e.cols.length);
        this.$set(this, "rows", rows);
      });
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.rows {
  display: flex;
  flex-direction: column;
  padding: 10px;
}
.row-ghost {
  background: #00c5db;
  min-height: 75px;
  max-width: 100%;
  padding: 0 !important;
  border: none;
  margin: 0 !important;
  border-radius: unset;
  display: flex;
  & > * {
    display: none;
  }
}
</style>
