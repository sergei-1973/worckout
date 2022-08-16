<template>
  <div class="row">
    <h2>Создать задачу</h2>
    <form @submit.prevent="submitHandler">
      <textarea
        name="text"
        oninput='this.style.height = "";this.style.height = this.scrollHeight + "px"'
        v-model="title"
        :maxlength="limit"
        class="input"
        type="text"
        placeholder="Название: лимит 520 символов"
        required
      />
      <p v-if="title.length > 0">{{ title.length }}</p>
      <textarea
        name="text"
        oninput='this.style.height = "";this.style.height = this.scrollHeight + "px"'
        v-model="description"
        :maxlength="limit"
        class="input"
        type="text"
        placeholder="Описание: лимит 520 символов"
        required
      />
      <p v-if="description.length > 0">{{ description.length }}</p>

      <input type="date" class="input" v-model="date" />

      <button class="btn" type="submit">Добавить</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
      limit: 520,
      date: null,
    };
  },
  methods: {
    submitHandler() {
      const task = {
        title: this.title,
        description: this.description,
        id: Date.now(),
        date: this.date,
        status: "active",
      };
      this.$store.dispatch("createTask", task);
      this.$router.push("/list");
    },
  },
};
</script>

<style scoped>
.row {
  margin: 20px auto auto;
  width: 500px;
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
</style>
