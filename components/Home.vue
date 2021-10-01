<template>
<div class="container pt-5"> 
  <h1 class="header-col" style='cursor:pointer'><span class="U-span">U</span>nsplash</h1>
  
    <form class='ml-2 pb-3 pt-4' @submit.prevent= "selectPhotos">
  <div class="input-container">
    <input class="" type="text" required  placeholder="Search Photos"
    v-model="myInput" />
    <!-- <button class="button btn  sub-btn" type="submit" @click.prevent= "selectPhotos">Search</button> -->
    <div>
         <button type="submit"  :disabled="mesg_in_submission"
          class="button btn btn-lg sub-btn">Send</button>
          </div> 
  </div>
</form>

 <div class="row">

    <NuxtLink to="" class="col-md-4" v-for="data in unsplashImg" :key="data.id">


  <img class="img-img w-100 mt-5" syle="border:5px solid pink"  :src="data.urls.regular" alt="image">

  </NuxtLink>
<!--
<div class="" v-for="data in unsplashImg" :key="data.id">
  <b-modal id="bv-modal-example" class="" style="border:none" hide-footer>
   
    <img class="img-img w-50 mt-5" stle="border:5px solid pink"  :src="data.urls.regular" alt="image">
   
  </b-modal>
  </div>-->
  </div>
  </div>
 

</template>

<script>
 
  import {  ref, useFetch, onMounted } from '@nuxtjs/composition-api';
  import axios from 'axios'
  export default {

  setup() {
    const unsplashImg = ref('')
    let clientId = ref('')
    let clientIdd = ref('')
    let myInput = ref('')
    let query = ref('')
    let mesg_in_submission= ref( false );


    // useFetch(async (e) => {
    //    let clientIdd=process.env.VUE_APP_API_KEY_TWO
    //      const url = `https://api.unsplash.com/search/photos?&query=flower&client_id=${clientIdd}`
    //     axios.get(url)
    //      .then( response => unsplashImg.value = response?.data.results)
    //   .catch(error => console.log(error))
    // })

    
    useFetch(async () => {
     let clientId=process.env.VUE_APP_API_KEY_TWO
      await axios.get(`https://api.unsplash.com/search/photos?&query=flower&client_id=${clientId}`)
      // await axios.get('https://api.unsplash.com/search/photos?query=flower&client_id=process.env.VUE_APP_API_KEY')
     .then( response => unsplashImg.value = response?.data.results)
    //  .then( console.log('hello', unsplashImg.value))
    //  .then(info=> console.log('hello', info))
      .catch(error => console.log(error))
    })



       const selectPhotos  = (e) => {
        let clientId=process.env.VUE_APP_API_KEY
        let query = myInput.value
        const url = `https://api.unsplash.com/search/photos?&query=${query}&client_id=${clientId}`
        axios.get(url)
         .then( response => unsplashImg.value = response?.data.results)
      .catch(error => console.log(error))

      mesg_in_submission.value = true;

      myInput.value=''
       }

    return { unsplashImg, selectPhotos, clientId, myInput,query, mesg_in_submission, clientIdd }
  }
}
  
</script>

<style scoped>

.header-col{
color:rgb(104, 103, 103);
}

.U-span{
font-style: italic;
font-size: 3rem;
color: rgb(255, 0, 128);
}

form {        
        width: 98%; 
       
    }
    .input-container {
        
        display: flex;
        background-color: #FFF;
        
        
    }

    input[type=text], .button {
        
        padding: .7rem 1rem;
    
    }
    
  
    input[type=text] {
        
        flex-grow: 2;
        
        outline: none;
        border: none;
        
        font-size: 1rem;
        
    }
    
    
    
    
    .button {
        background-color: rgb(285, 0, 128);
         color:whitesmoke;
        cursor: pointer;
        border-radius: 0.3rem 1rem 0.3rem 1rem;
        -webkit-transition: background-color .25s ease-in-out;
        -moz-transition: background-color .25s ease-in-out;
        -o-transition: background-color .25s ease-in-out;
        transition: background-color .25s ease-in-out;
        
    }
    
    .button:hover {     
        
        border: 2px solid  rgb(285, 0, 128);
      color: yellowgreen;
      background: inherit;
    }
   
    .button p { 
        color: #FFF;  
    }
    
    
    input[type=text]::placeholder {
        
        font-size: 1rem;
        
    }
</style>