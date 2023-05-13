<script>
import SingleProject from '../components/SingleProject.vue';
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'HomeView',
  components: { FilterNav, SingleProject },
  data() {
    return {
      projects: [],
      current: 'all'
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
    .then(response => response.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },

  methods: {
    handleDelete(id) {
       this.projects = this.projects.filter((project) => {
        return project.id !== id
      })
  },
   handleComplete(id){
    let p = this.projects.find(project => {
      return project.id === id
    })
    p.complete = !p.complete
   }
  }
   ,
   computed: {
    filteredProjects(){
      if (this.current === "completed"){
      return this.projects.filter(project => project.complete)
      }
      if (this.current === "ongoing"){
      return this.projects.filter(project => !project.complete)
      }
      return this.projects
   
   }


  }
  }

</script>

<template>
    <div class="home">
      <FilterNav @filterChange="current = $event" :current="current" style="margin-top:50px"/>
        <div v-if="projects.length">
         <div v-for="project in filteredProjects" :key="project.id" ><p><SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" /></p></div>
        </div>
    </div>
</template>



<style scoped>

</style>
