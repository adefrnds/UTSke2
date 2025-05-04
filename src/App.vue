<template>
  <div class="app">
    <h1>🎒 Persiapan Masuk Sekolah</h1>

    <div class="input-group">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambah kegiatan persiapan..." />
      <button @click="addTask">Tambah</button>
    </div>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="hideCompleted" />
        Tampilkan hanya kegiatan yang belum selesai
      </label>
    </div>

    <ul class="task-list">
      <li v-for="(task, index) in filteredTasks" :key="index">
        <input type="checkbox" v-model="task.done" />
        <span :class="{ done: task.done }">{{ task.text }}</span>
        <button class="delete" @click="removeTask(index)">🗑️</button>
      </li>
    </ul>

    <p v-if="tasks.length === 0">Belum ada kegiatan persiapan. Tambahkan yuk!</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [
        { text: 'Membeli seragam sekolah', done: false },
        { text: 'Menyiapkan alat tulis lengkap', done: false },
        { text: 'Mengatur ulang jadwal tidur', done: false },
        { text: 'Membuat jadwal belajar', done: false }
      ],
      hideCompleted: false
    };
  },
  computed: {
    filteredTasks() {
      return this.hideCompleted
        ? this.tasks.filter(task => !task.done)
        : this.tasks;
    }
  },
  methods: {
    addTask() {
      const text = this.newTask.trim();
      if (text) {
        this.tasks.push({ text, done: false });
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.app {
  max-width: 520px;
  margin: 40px auto;
  padding: 30px;
  background-color: #fffef6;
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  font-family: 'Segoe UI', sans-serif;
}

h1 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 20px;
}

.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 10px;
  border-radius: 6px;
  border: 1px solid #ddd;
  font-size: 16px;
}

button {
  background-color: #3498db;
  color: white;
  padding: 10px 14px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background-color: #2980b9;
}

.filter {
  margin-bottom: 15px;
  font-size: 14px;
  color: #555;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 12px;
  background-color: #ecf0f1;
  padding: 10px 14px;
  border-radius: 8px;
}

.task-list li span {
  flex-grow: 1;
  margin-left: 10px;
  font-size: 16px;
}

.task-list li span.done {
  text-decoration: line-through;
  color: #7f8c8d;
}

button.delete {
  background-color: #e67e22;
}

button.delete:hover {
  background-color: #d35400;
}
</style>
