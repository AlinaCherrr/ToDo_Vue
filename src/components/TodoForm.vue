<template>
  <form @submit.prevent class="todo-form">
    <div class="form-header">
      <h3>Новая задача</h3>
      <span class="hint">Добавьте то, что нужно сделать</span>
    </div>

    <div class="input-group">
      <input
        v-model="todo.title"
        class="input"
        type="text"
        placeholder="Название задачи..."
        required
      />
      <textarea
        v-model="todo.body"
        class="textarea"
        placeholder="Описание (необязательно)..."
        rows="2"
      />
    </div>
    
    <button 
      class="btn-create" 
      @click="createTodo"
      :disabled="!todo.title.trim()"
    >
      <span class="btn-icon">+</span>
      Добавить задачу
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      todo: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    createTodo() {
      if (!this.todo.title.trim()) return;
      
      this.$emit("create", { ...this.todo });
      this.todo = {
        title: "",
        body: "",
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.todo-form {
  background: linear-gradient(135deg, #ffffff 0%, #f8fafc 100%);
  border-radius: 20px;
  padding: 30px;
  margin-bottom: 40px;
  border: 1px solid #e8eef4;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  
  &:hover {
    box-shadow: 0 15px 35px rgba(145, 170, 190, 0.1);
  }
}

.form-header {
  margin-bottom: 25px;
  
  h3 {
    color: #6c879c;
    font-size: 1.4rem;
    font-weight: 500;
    margin-bottom: 8px;
  }
}

.hint {
  color: #a0b4c6;
  font-size: 0.95rem;
  font-style: italic;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.input, .textarea {
  width: 100%;
  border: 2px solid #e8eef4;
  padding: 16px 20px;
  border-radius: 14px;
  font-size: 1rem;
  color: #5d7b93;
  background: #ffffff;
  transition: all 0.3s ease;
  
  &:focus {
    outline: none;
    border-color: #b8d4ff;
    box-shadow: 0 0 0 4px rgba(184, 212, 255, 0.2);
  }
  
  &::placeholder {
    color: #b3c5d8;
  }
}

.textarea {
  resize: vertical;
  min-height: 60px;
  font-family: inherit;
  line-height: 1.5;
}

.btn-create {
  margin-top: 25px;
  width: 100%;
  padding: 18px;
  background: linear-gradient(135deg, #a8c6ff 0%, #8bb3ff 100%);
  color: white;
  border: none;
  border-radius: 14px;
  font-size: 1.1rem;
  font-weight: 500;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  transition: all 0.3s ease;
  
  &:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 10px 25px rgba(139, 179, 255, 0.3);
    background: linear-gradient(135deg, #9bbdff 0%, #7aa6ff 100%);
  }
  
  &:active:not(:disabled) {
    transform: translateY(0);
  }
  
  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
}

.btn-icon {
  font-size: 1.3rem;
  font-weight: 300;
}

@media (max-width: 768px) {
  .todo-form {
    padding: 25px;
  }
  
  .btn-create {
    padding: 16px;
  }
}
</style>