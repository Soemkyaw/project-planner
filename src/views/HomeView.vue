<template>
  <div v-for="project in projects" :key="project.id">
    <SingleProject :project="project" @completePjtStatus="completePjtStatus" @deletePjt="deletePjt"></SingleProject>
    
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject'
export default {
  components: { SingleProject },
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.projects = data;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    completePjtStatus(id) {
      let findProject = this.projects.find((project) => {
        return project.id === id
      })
      findProject.complete = !findProject.complete
    },
    deletePjt(id) {
      this.projects = this.projects.filter((project) => {
        return project.id != id
      })
    }
  },
};
</script>

<style scoped>

</style>
