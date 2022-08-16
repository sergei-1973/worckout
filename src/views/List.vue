<template>
  <div class="row">
    <h2>Список</h2>
    <label for="">Выбрать: </label>
    <select v-model="filter">
      <option value="">Choose your option</option>
      <option value="active">Активно</option>
      <option value="outdated">Просрочено</option>
      <option value="completed">Выполнено</option>
    </select>
    <button v-if="filter" style="margin-left: 10px" @click="filter = ''">
      очистить фильтр
    </button>
    <br />
    <br />
    <hr />

    <table v-if="tasks.length">
      <thead class="top">
        <tr>
          <th>#</th>
          <th>Название</th>
          <th>Описание</th>
          <th>Дата</th>
          <th>Статус</th>
          <th>Открыть</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, idx) in displayTasks" :key="task.id">
          <td>{{ idx + 1 }}</td>
          <td>{{ task.title }}</td>
          <td class="td">
            <div class="text">{{ task.description }}</div>
          </td>
          <td>{{ task.date }}</td>
          <td
            :class="{
              red: task.status == 'outdated',
              green: task.status == 'completed',
              blue: task.status == 'active',
            }"
          >
            {{ task.status }}
          </td>
          <td>
            <button>
              <router-link class="btn" :to="'/task/' + task.id"
                >Открыть</router-link
              >
            </button>
          </td>
          <td><button @click="removeTask(task.id)">&times;</button></td>
        </tr>
      </tbody>
    </table>
    <p class="p" v-else>No tasks</p>
  </div>
</template>

<script>
export default {
  data: () => ({
    filter: "",
  }),
  computed: {
    tasks() {
      return this.$store.getters.tasks;
    },
    displayTasks() {
      return this.tasks.filter((t) => {
        if (!this.filter) {
          return true;
        }
        return t.status === this.filter;
      });
    },
  },
  methods: {
    removeTask(id) {
      const elem = this.tasks.filter((t) => t.id === id);
      this.$store.dispatch("removeTask", elem);
    },
  },
};
</script>

<style sscoped>
h2 {
  margin-bottom: 20px;
}

.row {
  margin: 20px auto auto;
  max-width: 80%;
  margin-left: auto;
  margin-right: auto;
}
table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 20px;
}
td,
th {
  border-bottom: 1px solid teal;
  padding: 5px;
  text-align: justify;
}

.btn {
  padding: 5px;
  text-decoration: none;
  color: teal;
}
.td {
  max-width: 400px;
}
.text {
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
.p {
  margin-top: 50px;
  font-size: 50px;
}
.red {
  color: red;
}
.green {
  color: green;
}
.blue {
  color: blue;
}
</style>
