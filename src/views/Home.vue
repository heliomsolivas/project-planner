<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @deleteProject="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";
export default {
  name: "Home",
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  computed: {
    filteredProjects() {
      if (this.current === "completed") {
        return this.projects.filter((s) => s.complete);
      }
      if (this.current === "ongoing") {
        return this.projects.filter((s) => !s.complete);
      }

      return this.projects;
    },
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((s) => s.id !== id);
    },
    handleComplete(id) {
      let p = this.projects.find((s) => {
        return s.id === id;
      });
      p.complete = !p.complete;
    },
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
};
</script>
