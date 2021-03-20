<template>
  <div class="column">
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: "Column",
};
</script>
<style scoped>
.column {
  flex-grow: 1;
  border: 1px solid #ccc;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;
  font-size: 24px;
  border-radius: 4px;
  margin: 4px;
}
</style>