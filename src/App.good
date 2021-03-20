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
      <div v-for="row in rows" :key="row.id">
        <draggable
          fallbackOnBody
          :group="draggingRow? null : 'rows'"
          :swapThreshold="0.65"
          :value="row.cols"
          @input="inputRow(row.id, $event)"
          class="row"
          :class="{ dragging: draggingRow }"
          ghostClass="col-ghost"
          @start="draggingCol = row.id"
          @end="draggingCol = null"
        >
          <div
            v-for="col in row.cols"
            :key="col"
            class="col"
            :class="{ dragging: draggingCol === row.id }"
          >
            {{ col }}
          </div>
        </draggable>
      </div>
    </draggable>
  </div>
</template>

<script>
// TODO LIMIT 3 BLOCKS/ROW

import draggable from "vuedraggable";

export default {
  name: "App",
  components: {
    draggable,
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
      //this.$set(this, "rows", rows);
      // console.log(rows);
      console.log(JSON.stringify(value));
      const rows = [...value]
        .map((e) =>
          e.id && Array.isArray(e.cols) ? e : { id: this.id++, cols: [e] }
        )
        .filter((e) => e.cols.length);
      console.log("rowsAfter", JSON.stringify(rows));
      this.$set(this, "rows", rows);
    },
    inputRow(id, cols) {
      this.$nextTick().then(() => {
        console.log("rowsBefore", JSON.stringify(this.rows));
        const rows = [...this.rows]
          .map((e) => (e.id === id ? { id, cols } : e))
          .filter((e) => e.cols.length);
        this.$set(this, "rows", rows);
        console.log(id, cols);
        console.log(JSON.stringify(rows));
      });
    },
    inspect(code, event) {
      this.$emit(`x-${code}`, event);
      console.log(code, Object.keys(event));
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
  border: 1px solid #ccc;
  .row {
    cursor: pointer;
    display: flex;
    flex-direction: row;
    padding: 12px 16px;
    .col {
      flex-grow: 1;
      height: 32px;
      border: 1px solid red;
      padding-top: 15px;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 16px;
      font-size: 24px;
      border-radius: 4px;
      margin: 4px;
    }
  }
  .row-ghost {
    background: #00c5db;
    color: #00c5db;
    height: 75px;
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
  .col-ghost {
    background: red;
    max-height: unset;
    height: auto;
    flex-grow: 1;
    /* width: 32px !important;
    max-width: 32px;
    min-width: 32px; */
  }
}
</style>
