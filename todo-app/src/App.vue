<template>
  <div class="container">
    <div class="text-center mt-2">
        <h1 class="mb-2">Todo simple app</h1>
        <!-- <input type="text" @keydown.enter="filterTodos"> -->
          <ul v-for="todo in todoList" :key="todo.id">
            <li class="d-flex justify-content-between align-items-center" :style="{ marginBottom: '10px' }">
              <span :class="todo.completed === true ? 'underline' : ''">{{ todo.text }}</span>
              <div class="d-flex" :style="{ gap: '10px' }">
                <button class="green" @click="isDone(todo)">Done</button>
                <button class="red" @click="deleteItem(todo)">Delete</button>
              </div>
            </li>
          </ul>
          <span class="d-flex justify-content-end">Total {{ todoList.length }} items</span>
          <span class="d-flex justify-content-end">Completed: {{ itemCount() }} items</span>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      todoList: [
        {id: 1, text: "Learn Vue3.js", completed: false},
        {id: 2, text: "Learn React", completed: true},
        {id: 3, text: "Go gym", completed: false},
        {id: 4, text: "Read books", completed: false},
        {id: 5, text: "Watch series", completed: false},
      ]
    }
  },
  methods: {
    isDone(item) {
      item.completed = !item.completed;
    },
    deleteItem(item) {
      this.todoList = this.todoList.filter(t => t.id !== item.id);
    },
    itemCount() {
      let counter = 0;
      for(let i = 0; i < this.todoList.length; i++) {
        if(this.todoList[i].completed == true)
          counter++;
      }

      return counter;
    },
  }
}
</script>