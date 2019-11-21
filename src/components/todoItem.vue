<template>
  <li>
    <button class="btn btn-outline-gray todoItem" v-on:click="toggleState">{{ todo.text }}</button>
    <button class="btn btn-outline-primary todoDelete" v-on:click="$emit('remove', todo.id)">
      <i class="fa fa-trash-o fa-lg"></i>
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    toggleState(e) {
      var clickedElement = e.target;
      if (!(clickedElement.style.textDecoration === "line-through")) {
        clickedElement.style = "text-decoration: line-through;";
      } else {
        clickedElement.style = "";
      }
    }
  }
};
</script>




<style scoped>
.todoItem {
  width: 220px;
}
.todoDelete {
  width: 54px;
}
button:focus {
  color: #495057;
  background-color: #fff;
  border-color: #fff;
  outline: 0;
  box-shadow: 0 0 0 0.2rem rgba(0, 0, 0, 0);
}
</style>