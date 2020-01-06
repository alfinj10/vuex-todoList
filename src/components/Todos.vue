<template>
  <div>
    <div class="legend">
      <span>Double click to mark as complete</span>
      <span>
        <span class="incomplete-box"></span>
        = Incomplete
      </span>
      <span>
        <span class="complete-box"></span> = Complete
      </span>
    </div>
    <div class="todos">
      <div @dblclick='onDblClick(todo)' 
      v-for="todo in allTodos" 
      :key="todo.id" 
      class="todo" 
      v-bind:class="{'is-complete':todo.completed}">
        {{ todo.title }}
        <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  name: "Todos",
  methods: {
    ...mapActions(["fetchTodos", "deleteTodo","updateTodo"]),
    onDblClick(todo){
      const updatedTodo = {
        completed: !todo.completed,
        id: todo.id,
        title: todo.title
      }

      this.updateTodo(updatedTodo);

    }
  },
  computed: mapGetters(["allTodos"]),
  created() {
    this.fetchTodos();
  }
};
</script>

<style scoped>
.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}
.todo {
  border: 1px solid #ccc;
  background: #7db46cff;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
  position: relative;
  cursor: pointer;
}

i {
  position: absolute;
  bottom: 5px;
  right: 5px;
  color: #e7ebe0ff;
  cursor: pointer;
}

.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.complete-box {
    display: inline-block;
    width:10px;
    background: navy;
    height: 10px;
}

.incomplete-box {

    display: inline-block;
    width:10px;
    background: #7db46cff;
    height: 10px;

}

.is-complete {
  background: navy;
  color: white;
}

@media (max-width: 548px) {
    .todos {
        grid-template-columns: 1fr;
    }

    .legend {
        display: inline-block;
    }
}

</style>