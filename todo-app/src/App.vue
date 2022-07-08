<template>
  <div class="container">
    <div class="text-center mt-2">
        <h1 class="mb-2">Todo simple app</h1>
        <input type="text" v-model="todoText" @keydown.enter="addTodo(todoText)" placeholder="Add new todo item">
          <ul v-for="todo in filteredTodos" :key="todo.id">
            <li class="d-flex justify-content-between align-items-center" :style="{ marginBottom: '10px' }">
              <span :class="todo.completed === true ? 'underline' : ''">{{ todo.text }}</span>
              <div class="d-flex" :style="{ gap: '10px' }">
                <button class="green" @click="isDone(todo)">Done</button>
                <button class="red" @click="deleteItem(todo)">Delete</button>
              </div>
            </li>
          </ul>
          <span v-show="filteredTodos.length > 0" class="d-flex justify-content-end">Total: {{ filteredTodos.length }} items</span>
          <span v-show="itemCount() > 0" class="d-flex justify-content-end">Completed: {{ itemCount() }} items</span>
          <div class="d-flex justify-content-center align-items-center" :style="{ gap: '10px' }">
            <button @click="setFilterType('')">All items</button>
            <button @click="setFilterType('completed')">Completed items</button>
            <button @click="setFilterType('uncompleted')">Uncompleted items</button>
          </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      type: '',
      todoList: [
        {id: 1, text: "Learn Vue3.js", completed: false},
        {id: 2, text: "Learn React", completed: true},
        {id: 3, text: "Go gym", completed: false},
        {id: 4, text: "Read books", completed: false},
        {id: 5, text: "Watch series", completed: false},
      ]
    }
  },
  computed: {
    filteredTodos() {
      return this.todoList.filter(todo => {
        switch(this.type) {
          case 'completed':
            return todo.completed;
          case 'uncompleted':
            return !todo.completed;
          default:
            return true;
        }
      })
    }
  },
  methods: {
    addTodo(todoText) {
      this.todoList.push({ id: this._uid, text: todoText, completed: false});
      this.todoText = null;
    },
    isDone(item) {
      item.completed = !item.completed;
    },
    deleteItem(item) {
      this.todoList = this.todoList.filter(t => t.id !== item.id);
    },
    itemCount() {
      let counter = 0;
      for(let i = 0; i < this.filteredTodos.length; i++) {
        if(this.filteredTodos[i].completed == true)
          counter++;
      }

      return counter;
    },
    setFilterType(type) {
      this.type = type;
    }
  }
}
</script>