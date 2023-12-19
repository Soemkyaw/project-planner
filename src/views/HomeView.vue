<template>
  <FilterNav @filterProjects="current = $event" :current="current"></FilterNav>
  <div v-for="project in filterPjts" :key="project.id">
    <SingleProject
      :project="project"
      @completePjtStatus="completePjtStatus"
      @deletePjt="deletePjt"
    ></SingleProject>
  </div>
</template>

<script>
import FilterNav from "../components/FilterNav";
import SingleProject from "../components/SingleProject";
export default {
  components: {
    FilterNav,
    SingleProject,
  },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  computed: {
    filterPjts() {
      if (this.current === "complete") {
        return this.projects.filter((pjt) => {
          return pjt.complete;
        });
      }
      if (this.current === "ongoing") {
        return this.projects.filter((pjt) => {
          return !pjt.complete;
        });
      }
      return this.projects;
    },
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
        return project.id === id;
      });
      findProject.complete = !findProject.complete;
    },
    deletePjt(id) {
      this.projects = this.projects.filter((project) => {
        return project.id != id;
      });
    },
  },
};
</script>

<style scoped></style>
