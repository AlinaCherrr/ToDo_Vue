<template>
  <div class="app">
    <div class="container">
      <header class="header">
        <h1 class="title">Заметки</h1>
      </header>
      
      <todo-form @create="createTodo" />
      
      <div class="stats">
        <span class="stat-item">
          Всего: {{ todos.length }}
        </span>
        <span class="stat-item">
          Выполнено: {{ completedCount }}
        </span>
      </div>
      
      <todo-list 
        :todos="todos" 
        @toggle="toggleTodo"
        @remove="removeTodo"
      />
    </div>
  </div>
</template>

<script>
import TodoForm from "./components/TodoForm.vue";
import TodoList from "./components/TodoList.vue";

export default {
  components: {
    TodoForm,
    TodoList,
  },

  data() {
    return {
      todos: [
        { 
          id: 1, 
          title: "Изучить Vue.js", 
          body: "Пройти базовый курс", 
          completed: false,
          createdAt: new Date(2024, 0, 15)
        },
        { 
          id: 2, 
          title: "Купить продукты", 
          body: "Молоко, хлеб, фрукты", 
          completed: true,
          createdAt: new Date(2024, 0, 16)
        },
        { 
          id: 3, 
          title: "Позвонить маме", 
          body: "Обсудить планы на выходные", 
          completed: false,
          createdAt: new Date(2024, 0, 17)
        },
      ],
    };
  },

  computed: {
    completedCount() {
      return this.todos.filter(todo => todo.completed).length;
    }
  },

  methods: {
    createTodo(todo) {
      this.todos.push({
        ...todo,
        id: Date.now(),
        completed: false,
        createdAt: new Date()
      });
    },
    
    toggleTodo(id) {
      const todo = this.todos.find(t => t.id === id);
      if (todo) {
        todo.completed = !todo.completed;
      }
    },
    
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', -apple-system, sans-serif;
}

body {
  background: linear-gradient(135deg, #f5f7fa 0%, #e4e8f0 100%);
  min-height: 100vh;
  padding: 20px;
}

.app {
  max-width: 800px;
  margin: 0 auto;
}

.container {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 24px;
  padding: 40px;
  box-shadow: 0 10px 40px rgba(145, 170, 190, 0.15);
  backdrop-filter: blur(10px);
}

.header {
  text-align: center;
  margin-bottom: 40px;
}

.title {
  color: #5d7b93;
  font-size: 2.8rem;
  font-weight: 300;
  letter-spacing: -0.5px;
  margin-bottom: 12px;
}

.subtitle {
  color: #8da2b5;
  font-size: 1.1rem;
  font-weight: 400;
}

.stats {
  display: flex;
  justify-content: center;
  gap: 30px;
  margin: 30px 0;
  padding: 20px;
  background: #f8fafc;
  border-radius: 16px;
}

.stat-item {
  color: #7a8fa6;
  font-size: 1rem;
  display: flex;
  align-items: center;
  gap: 8px;
}

@media (max-width: 768px) {
  .container {
    padding: 25px;
  }
  
  .title {
    font-size: 2.2rem;
  }
  
  .stats {
    flex-direction: column;
    gap: 15px;
    align-items: center;
  }
}
</style>