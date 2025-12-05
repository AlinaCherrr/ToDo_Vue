<template>
  <div class="todo-list">
    <div class="list-header">
      <h3>Ваши задачи</h3>
      <span class="list-count">{{ todos.length }} задач</span>
    </div>
    
    <div class="list-content" v-if="todos.length">
      <todo-item 
        v-for="todo in todos" 
        :key="todo.id"
        :todo="todo"
        @toggle="$emit('toggle', todo.id)"
        @remove="$emit('remove', todo.id)"
      />
    </div>
    
    <div class="empty-state" v-else>
      <div class="empty-icon">📭</div>
      <h4>Нет задач</h4>
      <p>Добавьте свою первую задачу выше</p>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  components: { TodoItem },
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.todo-list {
  margin-top: 10px;
}

.list-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 25px;
  padding-bottom: 15px;
  border-bottom: 2px solid #f0f5fa;
  
  h3 {
    color: #6c879c;
    font-size: 1.4rem;
    font-weight: 500;
  }
}

.list-count {
  background: #f0f5fa;
  color: #8da2b5;
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 500;
}

.list-content {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.empty-state {
  text-align: center;
  padding: 60px 20px;
  color: #a0b4c6;
  
  .empty-icon {
    font-size: 4rem;
    margin-bottom: 20px;
    opacity: 0.5;
  }
  
  h4 {
    font-size: 1.4rem;
    font-weight: 500;
    margin-bottom: 10px;
    color: #8da2b5;
  }
  
  p {
    font-size: 1rem;
    max-width: 300px;
    margin: 0 auto;
    line-height: 1.5;
  }
}

@media (max-width: 768px) {
  .list-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }
}
</style>