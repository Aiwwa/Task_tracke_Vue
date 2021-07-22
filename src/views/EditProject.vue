<template>
    <form @submit.prevent="handleEdit">
    <label for="title">Title</label>
    <input type="text" v-model="title" required>

    <label for="details">Details</label>
    <textarea name="textarea" v-model="details" required></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return{
      title:'',
      details:'',
      uri: ' http://localhost:3000/projects/' + this.id 
    }
  },
  methods: {
    handleEdit(){
      fetch(this.uri, {
        method: 'PATCH',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({
          title: this.title,
          details: this.details
        })
      })
        .then(()=> this.$router.push('/'))
          .catch(err => alert(err))
    }
  },
  mounted() {
    fetch(this.uri)
      .then(res => res.json())
        .then(data => {
          this.title = data.title
          this.details = data.details
        })
  }
}
</script>

<style>

</style>