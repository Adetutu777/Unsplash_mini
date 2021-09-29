<template>
<div class="container pt-5">
  
  <NuxtLink to="/">
  <h1 class="header-col"><span class="U-span">U</span>nsplash</h1>
  </NuxtLink>
  <!-- <Modal-Popup /> -->


    <div class="pb-5" style=" margin: 0 auto;">
    <form class="" style="margin:0 auto"  >
    <input class="w-75 py-2" style="border:3px solid red; margin:0 auto" type="text" placeholder="search photos" v-model="myInput">
   <button type="submit" @click.prevent= "selectPhotos"
                       class="btn  sub-btn" style="border:1px solid red">search </button>
    </form>
    </div>

  <div class="row">

    <div class="col-md-4"  v-for="data in unsplashImg" :key="data.id">
<b-button id="show-btn" class="pt-0" style="background:none; border:none" @click="$bvModal.show('bv-modal-example')">

  <img class="img-img w-100 mt-5" style="border:5px solid pink"  :src="data.urls.regular" alt="image">
     <!-- <p> {{ data.description }} </p> -->
       </b-button>
  </div>

<div class="" v-for="data in unsplashImg" :key="data.id">
  <b-modal id="bv-modal-example" class="" style="border:none" hide-footer>
   
    <img class="img-img w-50 mt-5" style="border:5px solid pink"  :src="data.urls.regular" alt="image">
    <h3>{{data.bio}}</h3>
    hello
  </b-modal>
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
    // let mesg_in_submission= ref( false );
    let clientId = ref('')
    let myInput = ref('')
    let query = ref('')

     

    useFetch(async () => {
      await axios.get('https://api.unsplash.com/search/photos?query=nature&client_id=8ol4_VssgaET9oFTpTaMB85YaM38KmeqCh4gDjIezmY')
     .then( response => unsplashImg.value = response?.data.results)
    //  .then( console.log('hello', unsplashImg.value))
    //  .then(info=> console.log('hello', info))
      .catch(error => console.log(error))
    })

  //   const invalidFeedback = computed(() => {
  //  if (name.value.length > 0) {
  //        return 'Enter at least 4 characters.'
  //       }
  //     return  'Please enter something.'
    
  // })

       const selectPhotos  = (e) => {
        let clientId='8ol4_VssgaET9oFTpTaMB85YaM38KmeqCh4gDjIezmY'  
        let query = myInput.value
        // let url = 'https://api.unsplash.com/search/photos?&client_id=" +clientId + "&query="+query';
        // const url = `${url}&query=${query}&client_id=${clientId}`;
        const url = `https://api.unsplash.com/search/photos?&query=${query}&client_id=${clientId}`
        axios.get(url)
         .then( response => unsplashImg.value = response?.data.results)
        console.log('hello', query)
        console.log(e)
    //  .then( response => unsplashImg.value = response?.data.results)
    //  .then( console.log('hello', unsplashImg.value))
    //  .then(info=> console.log('hello', info))
      // .catch(error => console.log(error))

      // mesg_in_submission.value = true;
       }

 
  myInput.value=''


     
    return { unsplashImg, selectPhotos, clientId, myInput,query }
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



