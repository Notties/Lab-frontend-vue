<template>
  <!-- <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <li v-for="(item) in todoData" :key="item">
    {{ item.Name }}
  </li> -->
  <div>
    ใส่น้ำหนัก
    <input v-model="weight" />
    <br />
    ใส่ส่วนสูง
    <input v-model="height" />

    <br />
    <button @click="getBmi">คำนวณ BMI</button>
    <br />
    <br />
    {{ resBmi }}
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},

  data() {
    return {
      todoId: 1,
      todoData: null,
      resBmi: null,
      height: 0,
      weight: 0,
    };
  },

  methods: {
    async fetchData() {
      this.todoData = null;
      const res = await fetch(`http://127.0.0.1:8000/`);
      this.todoData = await res.json();
    },
    async getBmi() {
      const res = await fetch(
        `http://127.0.0.1:8000/get_bmi/${this.height}-${this.weight}`
      );
      this.resBmi = await res.json();
    },
  },

  mounted() {
    this.fetchData();
  },

  watch: {
    todoId() {
      this.fetchData();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
