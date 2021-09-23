<template>
<div class="container pt-5">
  
  <NuxtLink to="/">
  <h1 class="header-col"><span class="U-span">U</span>nsplash</h1>
  </NuxtLink>
  <!-- <div>
    <b-form-group
      id="fieldset-1"
      description="Let us know your name."
      label="Enter your name"
      label-for="input-1"
      valid-feedback="Thank you!"
      :invalid-feedback="invalidFeedback"
     
    >
      <b-form-input id="input-1" v-model="name" :state="state" trim></b-form-input>
    </b-form-group>
  </div> -->
    
    <div class="pb-5" style=" margin: 0 auto;">
    <form class="" @click.prevent= "selectPhotos"  >
    <input class="w-75" type="text" placeholder="search photos">
    <button class=""  >search</button>
    </form>
    </div>

  <div class="row">
  

  <div class="col-md-4" v-for="data in unsplashImg" :key="data.id">
  <img class="img-img w-100 pt-3"  :src="data.urls.regular" alt="image">
     <!-- <p> {{ data.description }} </p> -->
  </div>
  </div>
  </div>
</template>

<script>
 
  import {  ref, useFetch } from '@nuxtjs/composition-api';
  import axios from 'axios'
  export default {

  setup() {
    const unsplashImg = ref('')
    // const name = ref('')

     

    useFetch(async () => {
     unsplashImg.value = await axios.get('https://api.unsplash.com/search/photos?query=nature&client_id=8ol4_VssgaET9oFTpTaMB85YaM38KmeqCh4gDjIezmY')
     .then( response => unsplashImg.value = response?.data.results)
    //  .then( console.log('hello', unsplashImg.value))
    //  .then(info=> console.log('hello', info))
      .catch(error => console.log(error))
          // .then(response => response.json())
          // .then((res) => res.json())
    })

  //   const invalidFeedback = computed(() => {
  //  if (name.value.length > 0) {
  //        return 'Enter at least 4 characters.'
  //       }
  //     return  'Please enter something.'
    
  // })

       const selectPhotos  = (e) => {
        //  console.log('hi')
        unsplashImg.value =  axios.get('https://api.unsplash.com/search/photos?query=images&client_id=8ol4_VssgaET9oFTpTaMB85YaM38KmeqCh4gDjIezmY')
     .then( response => unsplashImg.value = response?.data.results)
    //  .then( console.log('hello', unsplashImg.value))
    //  .then(info=> console.log('hello', info))
      .catch(error => console.log(error))
       }

 
  


     
    return { unsplashImg, selectPhotos}
    // return { unsplashImg, invalidFeedback, name }
  }
}
  
</script>

<style scoped>
.form-grp{
    margin: 0 auto;
    
    
}

.header-col{
color:rgb(104, 103, 103);
}

.U-span{
font-style: italic;
font-size: 3rem;
color: rgb(255, 0, 128);
}
</style>