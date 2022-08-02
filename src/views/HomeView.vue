<template>
  <Home />
  <div v-if="projects.length">
    <div v-for="item in projects" :key="item.id">
      <SingleProductPage :prop="item" @deleteFromHomeProject="handleDelete" @completeChanger="handleComplete"  />
    </div>

  </div>
</template>

<script>
import SingleProductPage from '../components/SinglePrPage.vue'


export default {
  components: { SingleProductPage  },
  data() {
    return {
      projects: []
    }
  },
  mounted() {
    fetch('http://localhost:3000/jsonproject')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  methods:{
    handleDelete(removeId){
    this.projects = this.projects.filter(i => {
      return i.id !== removeId
    })
    },
    handleComplete(CompId){
      let p = this.projects.find(item => {
        return item.id === CompId
      })
      p.complete = !p.complete
    }
  }
  
}
</script>

<style>

</style>