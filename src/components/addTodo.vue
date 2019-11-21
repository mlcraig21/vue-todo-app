<template>
  <div class="addTodo">
    <input
      type="text"
      placeholder="Add a new todo item"
      :value="value"
      v-on="listener"
      class="form-control"
    >
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: ""
    }
  },
  computed: {
    listener() {
      return {
        ...this.$listener,
        // Override input listener to work with v-model
        input: event => this.$emit("input", event.target.value)
      };
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.addTodo {
  display: inline-flex;
}
</style>
