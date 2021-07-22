<template>
  <form @submit.prevent="handleSubmit">
    <label for="title">Title</label>
    <input type="text" v-model="title" required>

    <label for="details">Details</label>
    <textarea name="textarea" v-model="details" required></textarea>
    <button>Add project</button>
  </form>
</template>

<script>
export default {
  data() {
    return{
      title:'',
      details:''
    }
  },
  methods: {
    handleSubmit(){
      let project = {
        title: this.title,
        details: this.details,
        complete: false,
      }
      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(project)
      })
        .then(()=> this.$router.push('/'))
         .catch(err => alert(err))
    }
  }
}
</script>

<style>
  form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  label {
    display: block;
    color: rgb(50, 50, 50);
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    background-color: rgb(50, 50, 50);
    color:azure;
    padding: 15px 30px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
  }
</style>