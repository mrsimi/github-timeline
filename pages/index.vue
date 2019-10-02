<template>
<div id="container">
  <h1>Github Timeline</h1>
  <div id="search-panel">
     <a-input-search
      placeholder="input username"
      @search="onSearch"
      enterButton
      />
  </div>
   <blockquote>
                <p>You cannot dream yourself into a character; 
                you must hammer and forge yourself one </p>
                <footer> David Thoreau</footer>
    </blockquote>
    
    <div id="timeline-container" v-show="!errorState">
      <a-timeline>
        <timeline-card v-for="(repo, index) in repos" :key="index"
          :name="repo.name"
          :description="repo.description"
          :html_url="repo.html_url"
          :created_at="repo.created_at"
          :open_issues_count="repo.open_issues_count"
          :language="repo.language"
          :forks_count="repo.forks_count">
        </timeline-card>
      </a-timeline>
    </div>
    
   
    <div v-show="errorState" class="error">
      <h1>404</h1>
      <p>user not found</p>
    </div>

</div>
</template>

<script>
import TimelineCard from '~/components/Timeline.vue'

export default {
  components:{
    TimelineCard
  },
  data(){
    return{
      searchQuery: "",
      repos: [],
      errorInput: false,
      errorState: false,
      
    }
  }, 
  methods: {
    onSearch(value){
      if(value === ""){
        this.errorInput = true
      }
      else{
        const URL= 'https://api.github.com/users/'+value+'/repos';
        this.$axios.$get(URL)
            .then(response => {
              this.repos = response
              this.errorState = false;
            })
            .catch(e => {
              this.errorState = true
            })
      }
     
    }
  }
}
</script>


<style scoped>
#search-panel{
  margin: 0 auto;
  width: 300px;
  padding-bottom: 20px;
}

#container{
  padding: 50px;
}

#container > h1{
  text-align: center;
  padding-bottom: 20px;
}

#timeline-container{
  margin: 0 auto;
  width: 80%;
  padding-top: 20px;
}

blockquote{
  margin: 0 auto;
  width: 320px;
  padding: 10px;
  text-align: center;
}

.error{
  text-align: center;
  margin: 10%;
}

.error > h1{
  font-size: 500%;
}
</style>