<template>
  <nav class="filter-projects">
    <button 
      @click="updateFilter('all')"
      :class="{active: current === 'all'}"
      >View All</button>
    <button 
      @click="updateFilter('completed')"
      :class="{active: current === 'completed'}"
      >Completed</button>
    <button 
      @click="updateFilter('ongoing')"
      :class="{active: current === 'ongoing'}"
      >Ongoing</button>
  </nav>
</template>
   
<script>
export default {
  props: ['current'],
  methods: {
    updateFilter(by){
      this.$emit('filterChange', by)
    }
  }
}
</script>

<style>
  .filter-projects {
    display: flex;
    justify-content: center;
    margin-bottom: 40px ;
  }

  button {
    margin: 0 5px;
    padding: 10px 20px;
    border: none;
    background-color: rgb(50, 50, 50);
    color: rgb(254, 255, 240);
    border-radius: 30px;
    font-weight: 900;
  }
  .active{
    color:rgb(255, 140, 0);
  }
</style>