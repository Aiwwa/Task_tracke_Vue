<template>
  <div class="home">
    <FilterProjects @filterChange="current = $event" :current="current"/>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete='handleDeleteProject' @complete='handleComplete'/>
      </div>
    </div>
  </div> 
</template>

<script>
import SingleProject from '../components/SingleProject.vue'
import FilterProjects from '../components/FilterProjects.vue'

export default {
  name: 'Home',
  data(){
    return{
      projects:[],
      current: 'all'
    }
  },
  components: { 
    SingleProject,
    FilterProjects
  },
  methods: {
     handleDeleteProject(id){
       this.projects = this.projects.filter((project) => project.id !== id)
     },
     handleComplete(id){
       let projetComplete = this.projects.find(project => project.id === id)
       projetComplete.complete = !projetComplete.complete
     }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => alert(err.message))
  },
  computed: {
    filteredProjects(){
      if(this.current === 'completed') {
        return this.projects.filter(project => project.complete)
      } 
      if(this.current === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      } 
      return this.projects
    }
  },
}
</script>

<style >
  body {
    background: rgb(230, 230, 230);
  }
</style>
