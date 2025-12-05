<template>
  <div class="todo-item" :class="{ completed }">
    <div class="todo-content">
      <div class="todo-checkbox" @click="$emit('toggle')">
        <div class="checkbox" :class="{ checked: completed }">
          <span v-if="completed">✓</span>
        </div>
      </div>
      
      <div class="todo-text">
        <div class="todo-title">
          {{ todo.title }}
        </div>
        <div class="todo-body" v-if="todo.body">
          {{ todo.body }}
        </div>
        <div class="todo-date">
          {{ formatDate(todo.createdAt) }}
        </div>
      </div>
      
      <button class="btn-delete" @click="$emit('remove')" title="Удалить">
        X
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  
  computed: {
    completed() {
      return this.todo.completed;
    }
  },
  
  methods: {
    formatDate(date) {
      if (!date) return '';
      const d = new Date(date);
      return d.toLocaleDateString('ru-RU', {
        day: 'numeric',
        month: 'short',
        year: 'numeric'
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.todo-item {
  background: white;
  border-radius: 18px;
  padding: 25px;
  border: 2px solid #f0f5fa;
  transition: all 0.3s ease;
  
  &:hover {
    box-shadow: 0 10px 30px rgba(145, 170, 190, 0.12);
    border-color: #e8eef4;
  }
  
  &.completed {
    opacity: 0.8;
    background: #fafcff;
    
    .todo-title {
      text-decoration: line-through;
      color: #a0b4c6;
    }
  }
}

.todo-content {
  display: flex;
  align-items: flex-start;
  gap: 20px;
}

.todo-checkbox {
  cursor: pointer;
  flex-shrink: 0;
}

.checkbox {
  width: 28px;
  height: 28px;
  border: 2px solid #dce4ed;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  
  &.checked {
    background: linear-gradient(135deg, #a8c6ff 0%, #8bb3ff 100%);
    border-color: #8bb3ff;
    
    span {
      color: white;
      font-size: 1rem;
      font-weight: bold;
    }
  }
}

.todo-text {
  flex: 1;
}

.todo-title {
  color: #5d7b93;
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 8px;
  line-height: 1.4;
  transition: color 0.3s ease;
}

.todo-body {
  color: #8da2b5;
  font-size: 1rem;
  line-height: 1.5;
  margin-bottom: 12px;
}

.todo-date {
  color: #b3c5d8;
  font-size: 0.85rem;
  display: flex;
  align-items: center;
  gap: 6px;
}

.btn-delete {
  flex-shrink: 0;
  width: 44px;
  height: 44px;
  border-radius: 12px;
  border: none;
  background: #fff5f5;
  color: #ff9a9a;
  font-size: 1.2rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  
  &:hover {
    background: #ffeaea;
    transform: scale(1.05);
  }
  
  &:active {
    transform: scale(0.95);
  }
}

@media (max-width: 768px) {
  .todo-item {
    padding: 20px;
  }
  
  .todo-content {
    gap: 15px;
  }
  
  .checkbox {
    width: 24px;
    height: 24px;
  }
}
</style>