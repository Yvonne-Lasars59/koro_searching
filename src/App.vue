
<template>
  <div class="toppanel">
    <h2>
      Search for the Images of your Dream
    </h2>
  </div>
  <div class="row">
    <div class="column" >
      <div>
        <div class="inputbox"  >
          <h3 class = "subheader">What are you looking for?</h3>
          <input v-model="search_key" 
            @input="update_foto_list" 
            />
        </div>
        
      </div>
    </div>

    <div class="column" >
      <h3 class="subheader">Results:</h3>
      <div class = "flexbox-container" >
        <div v-for = "foto in foto_list" :key="foto">
          <div class = "flexbox-item">
            <img :alt="alt_msg"  
              :src="foto.urls.thumb" 
              height="120" />
          </div>  
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import _ from 'lodash'
const unsplash_id = "8M-tyYIE-Mlbmc5vSmJuvUVXcURAs0umAm9f8OGqoUM"


export default {
  name: "app",
  data(){
    return{
      search_key: "peanut butter?",
      alt_msg: "no foto",
      foto_list: [],
    };
  },
  methods:{
    update_foto_list: function(){
      let key = this.search_key

      axios.get(`https://api.unsplash.com/search/photos?query=${key}&client_id=${unsplash_id}`)
        .then(response => {
          this.foto_list = response.data.results
        })
        .catch(e => {
          console.log(e)
        })
    }
  }
}

</script>


<style scoped>
.flexbox-container{
    display: flex; 
    flex-wrap: wrap;
    justify-content: center;
    align-content: center;
  }
.flexbox-item{
  margin: 5px;
}

.subheader{
  text-align: center;
}

.inputbox{
  padding: 10px;
  display: grid; 
  place-items: center;
}

.toppanel{
  padding: 10px 0px;
  background-color: #ffebcd ;
  text-align: center;
}

@media (min-width: 1024px) {
  .row {
    display: flex;
  }

  .column {
    flex: 50%;
  }

}
</style>
