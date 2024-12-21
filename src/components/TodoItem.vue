<template>
    <div class="todo-item">
        <input 
            type="checkbox" 
            :checked="todo.completed"
            @change="$emit('update', { ...todo, completed: !todo.completed })" 
        />
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="$emit('remove')">Remove</button>
    </div>
</template>

<script>
export default {
    props: {
        todo: Object
    }
};
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  padding: 12px 16px;
  background: #f8fafc;
  border-radius: 8px;
  transition: all 0.2s ease;
}

.todo-item:hover {
  background: #f1f5f9;
  transform: translateX(4px);
}

input[type="checkbox"] {
  width: 20px;
  height: 20px;
  margin-right: 12px;
  cursor: pointer;
}

span {
  flex: 1;
  font-size: 1rem;
  color: #2c3e50;
}

.completed {
  text-decoration: line-through;
  color: #94a3b8;
}

button {
  background: #ef4444;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.875rem;
  transition: all 0.2s ease;
}

button:hover {
  background: #dc2626;
  transform: scale(1.05);
}

button:active {
  transform: scale(0.95);
}

@media (max-width: 480px) {
  .todo-item {
    padding: 10px;
  }
  
  button {
    padding: 6px 12px;
    font-size: 0.8rem;
  }
}
</style>