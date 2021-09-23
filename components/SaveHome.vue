<template>
    <div>
    <h1>Unsplash</h1>
    <div>
   
    <div class="form-grp">
    <input type="text" class="w-75 " placeholder="search photos">
    </div>
 
  </div>
  {{$fetchState}}
   <div class="columny px-2 mb-r" v-for= "data in unsplashImg" :key="data.id">
                          <div class="cad about-me pb-0" >  
                          
                          
                          <p class="text-center text-white size-text">  {{data.description}} </p>
                          <p>hello</p>
                        </div>
                        </div>



    </div>
</template>

<script>
  // export default {
  //     data() {
  //         return {
  //               name: ''
  //         }
  //     },
  //   computed: {
  //     state() {
  //       return this.name.length >= 4
  //     },
  //     invalidFeedback() {
  //       if (this.name.length > 0) {
  //         return 'Enter at least 4 characters.'
  //       }
  //       return 'Please enter something.'
  //     }
  //   }
  // }
  import {  ref, useFetch } from '@nuxtjs/composition-api';
  import axios from 'axios'
  export default {
  //   setup() {
  //   const unsplashImg = ref('')

  //   const { fetch, fetchState } = useFetch(async () => {
  //     unsplashImg.value = await axios.get('https://api.unsplash.com/search/photos?query=images&client_id=8ol4_VssgaET9oFTpTaMB85YaM38KmeqCh4gDjIezmY')
  //   })

  
  //   fetch()

 
  //   fetchState

  //   return { unsplashImg}
  // },

  setup() {
    const unsplashImg = ref('')

    
    useFetch(async () => {
     unsplashImg.value = await axios.get('https://api.unsplash.com/search/photos?query=images&client_id=8ol4_VssgaET9oFTpTaMB85YaM38KmeqCh4gDjIezmY')
     .then( response => console.log('hello', response.data.results))
     .then( response => unsplashImg.value = response?.data.results)
   .catch(error => console.log(error))
    })

    return { unsplashImg }
  },
}
  
</script>

<style scoped>
.form-grp{
    margin: 0 auto;
    
}
</style>