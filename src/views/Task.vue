<template>
  <div>
    <div v-if="task" class="row">
      <h2>{{ task.title }}</h2>
      <form @submit.prevent="submitHandler">
        <textarea
          v-model="description"
          type="text"
          class="input"
          name="text"
          oninput='this.style.height = "";this.style.height = this.scrollHeight + "px"'
        />

        <p v-if="description.length > 0">{{ description.length }}</p>

        <input type="date" class="input" v-model="date" />

        <div class="button" v-if="task.status !== 'completed'">
          <button class="btn" type="submit">Update</button>
          <button @click="completeTask" class="btn" type="button">
            Complete task
          </button>
        </div>
      </form>
    </div>
    <p v-else>Task not found</p>
  </div>
</template>

<script>
export default {
  computed: {
    task() {
      return this.$store.getters.taskById(+this.$route.params.id);
    },
  },
  data() {
    return {
      description: "",

      date: null,
    };
  },
  mounted() {
    this.description = this.task.description;
    this.date = this.task.date;
  },
  methods: {
    submitHandler() {
      this.$store.dispatch("updateTask", {
        id: this.task.id,
        description: this.description,
        date: this.date,
      });
      this.$router.push("/list");
    },
    completeTask() {
      this.$store.dispatch("completeTask", this.task.id);
      this.$router.push("/list");
    },
  },
};
</script>

<style scoped>
.row {
  margin: 20px auto auto;
  width: 800px;
  text-align: center;
}
form {
  display: flex;
  flex-direction: column;
}

.input {
  margin: 20px 0px 10px 0px;
  padding: 15px;
  border-radius: 4px;
  border: 1px solid teal;
  font-size: 17px;
}
.input:hover {
  background-color: #f0ffff;
}
.btn {
  margin-top: 20px;
  padding: 5px;
  width: 40%;
  border: 1px solid teal;
  border-radius: 4px;
  background-color: white;
}
.btn:hover {
  background-color: #c0ffff;
  color: black;
}
.button {
  display: flex;
  flex-direction: column;
}
</style>
