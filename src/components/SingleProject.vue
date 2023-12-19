<template>
  <div class="singleProject" :class="{ donePjt: project.complete }">
    <div class="flexing">
      <h3 class="title" @click="showDetail = !showDetail">
        {{ project.title }}
      </h3>
      <h3 class="icons">
        <i class="fa-solid fa-trash" @click="deleteProject"></i>
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <i class="fa-solid fa-pen"></i>
        </router-link>
        <i class="fa-solid fa-circle-check " @click="completeStatus" :class="{active: project.complete}"></i>
      </h3>
    </div>
    <p v-if="showDetail">{{ project.detail }}</p>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
    };
  },
  methods: {
    completeStatus() {
      fetch("http://localhost:3000/projects/" + this.project.id, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
      })
        .then(() => {
          this.$emit("completePjtStatus", this.project.id);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    deleteProject() {
      fetch("http://localhost:3000/projects/" + this.project.id, {
        method: "DELETE",
      })
        .then(() => {
          this.$emit("deletePjt", this.project.id);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
.singleProject {
  background-color: #eae3e3;
  padding: 20px;
  margin-bottom: 10px;
  border-radius: 8px;
  border-left: 6px solid crimson;
  /* border-left: 6px solid rgb(227, 193, 72); */
}
.title {
  color: indigo;
  cursor: pointer;
}
.fa-pen {
  color: #2c3e50;
}
.flexing {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.icons i {
  margin-left: 10px;
  cursor: pointer;
}
.fa-trash{
  color: red;
}
.fa-pen{
  color: #40a6ce;
}
.fa-circle-check{
  color: crimson;
}
.icons i:hover {
  opacity: 0.33;
}
.donePjt {
  border-left-color: rgb(24, 146, 13);
}
.active{
  color: rgb(24, 146, 13);
}
</style>
