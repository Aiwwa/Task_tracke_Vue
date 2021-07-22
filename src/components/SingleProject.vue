<template>
  <div class="project" :class="{complete: project.complete}">
      <div  class="project__action">
        <h3 @click="toggleProjectDetails"> {{project.title}}</h3>
        <div class="action__icons">
          <router-link :to="{name: 'EditProject', params:{ id: project.id}}">
            <span class="material-icons edit">edit</span>
          </router-link>
          <span @click="toggleComplete" class="material-icons" :class="{done: project.complete}">done</span>
          <span @click="deleteProject" class="material-icons">delete</span>
        </div>
      </div>
      <div v-if="showProjectDetails" class="project__details">
        <p>{{project.details}}</p>
      </div>
      <div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['project'],
  data(){
    return {
      showProjectDetails: false,
      uri: "http://localhost:3000/projects/" + this.project.id
    }
  },
  methods: {
    toggleProjectDetails(){
      this.showProjectDetails = !this.showProjectDetails
    },
    toggleComplete(){
      fetch(this.uri, {
        method: 'PATCH',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({complete: !this.project.complete})
      })
        .then(() => this.$emit('complete', this.project.id))
          .catch(err => alert(err))
    },
    deleteProject(){
      fetch(this.uri, {method: 'DELETE'})
        .then(() => this.$emit('delete', this.project.id))
          .catch(err => alert(err))
    }
  }
}
</script>

<style>
.project{
  margin: 20px auto;
  padding: 10px 20px;
  border-left: 5px solid tomato ;
  background-color: rgb(50, 50, 50);
  color: rgb(254, 255, 240);
  -webkit-box-shadow: -7px 9px 12px -1px rgba(0,0,0,0.23); 
  box-shadow: -7px 9px 12px -1px rgba(0,0,0,0.23);
}

h3 {
  cursor: pointer;
}

.complete{
  border-left: 5px solid rgb(191, 255, 0);
}

.project__action{
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.action__icons span{
  margin: 0 10px;
}
.action__icons span:hover{
  color: rgb(255, 140, 0);
  cursor: pointer;
}

.done  {
  color: rgb(191, 255, 0);
}

.edit {
  color: azure;
}


</style>