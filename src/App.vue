<template>
  <div>
    <h1 :style="{ textDecoration: decoration }" class="todo">Todo List</h1>
    <p>V-model: {{ name }}</p>
    <input type="text" v-model="name" />
    <br />
    V-bind:
    <a :href="link">Link Teste</a>
    <h1>Minha lista:</h1>
    <button @click="showList = !showList">Ver lista</button>
    <ul v-if="showList">
      <li
        v-for="(task, index) in tasks"
        @dblclick="complete(task)"
        :key="index"
        class="task-item"
        :class="{
          'line-through': task.isDone,
        }"
      >
        {{ task.name }}
        <button @click="remove(task)">&times;</button>
      </li>
    </ul>

    <br />
    <input
      placeholder="Adicionar item"
      type="text"
      v-model="currentTask"
      @keyup.enter="addTask"
      v-focus
    />
  </div>
</template>

<script>
export default {
  directives: {
    focus: {
      inserted: function (el) {
        el.focus();
      },
    },
  },
  data() {
    return {
      currentTask: "",
      name: "Igor",
      link: "https://google.com.br",
      decoration: "underline",
      showList: true,
      tasks: [
        { name: "Curso de Php 8", isDone: false },
        { name: "Curso de Html5", isDone: true },
      ],
    };
  },
  methods: {
    addTask() {
      this.tasks.push({
        name: this.currentTask,
        isDone: false,
      });
      this.currentTask = "";
    },
    remove(task) {
      this.tasks = this.tasks.filter((t) => t.name !== task.name);
    },
    complete(task) {
      this.tasks = this.tasks.map((t) => {
        if (t.name === task.name) {
          return { ...t, isDone: !t.isDone };
        }
        return { ...t };
      });
    },
  },
};
</script>

<style>
body {
  font-family: "Trebuchet MS";
}
.todo {
  background-color: #495057;
  color: white;
  border-radius: 0.25rem;
  text-align: center;
  padding: 10px 0;
}
.line-through {
  text-decoration: line-through;
}
.task-item {
  cursor: pointer;
}
a {
  color: white;
  border-color: #007bff;
  background-color: #007bff;
  display: block;
  border-radius: 0.25rem;
  padding: 5px;
  text-align: center;
}
button {
  cursor: pointer;
  color: #fff;
  border-color: #007bff;
  background-color: #007bff;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
}
input {
  display: block;
  width: 100%;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #495057;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
  width: 90%;
  margin: 0 auto;
}
</style>