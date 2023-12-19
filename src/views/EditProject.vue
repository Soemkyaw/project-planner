<template>
  <form @submit.prevent="editProject">
    <label>Title</label>
    <input type="text" v-model="title" />
    <label>Detail</label>
    <input type="text" v-model="detail" />
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      detail: "",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects/" + this.id)
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.title = data.title;
        this.detail = data.detail;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    editProject() {
      fetch("http://localhost:3000/projects/" + this.id, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
        }),
      })
        .then(() => {
          this.$router.push({ name: "home" });
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
button {
  background-color: #e3e330;
}
</style>
