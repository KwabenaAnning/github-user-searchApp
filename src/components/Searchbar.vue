<script setup>
import GitDetails from '../components/GitDetails.vue';
import { ref } from "vue";
import axios from "axios";
import moment from "moment";

console.log ('search')

const username = ref("")
const user = ref (null)
const userNotFound = ref(false);
const loading = ref(false)

const searchUser = async () => {
    if (username.value.trim() ===""){
        // .trim() is to remove whitespaces because in prog white spaces are part of code and there are assigned a value.
        // .trim will allow us get exactly, the git username.
        alert("Please Enter a gitHub username.");
        return;
        // return means you are returning what is in the function to a variable but it will not be seen.
        // to be seen we need to console.log to see reults.
    }

    // naturally, the loading should be false because we do not want it to be loading when we have not searched anything.
    // true means it has been assigned a task to take so he should go ahead.
    console.log('searching...')
    loading.value = true;
    try{
        const feedback = await axios.get(
            // to make an axios request, we use the .get method. to push a information we use the .post method and to delete, we use the .delete method.
        //    we want the info of github users hence, .get method
            `https://api.github.com/users/${username.value}`
        );
    user.value = feedback?.data;
    // this is a shorter form of tenary operator response.data is also going to work but for security reasons we go with the question mark. like say you are seeking permission before you grab the info.
    loading.value = false;
    console.log(feedback?.data);
    // thpart means that the lader will stop if the results come 
    } catch(error) {
      // this part is mostly used for taking in negative results. eg error
        console.error('Error:',error);
        user.value = null;
        userNotFound.value =true;
        loading.value = false;
        // alert('User not found or an error occurred.');
    }
};
</script>

<template>
  <div class="container" >
    <div class="headSaearch">
        <header>
        <div class="header">
            <!-- <img src="@." alt=""> -->
            <h2>devfinder</h2>
            <h5>Dark</h5>
        </div>
        </header>
        <div class="searchPlace">
            <div class="search">
                <img src="@/assets/searchIcons.png" alt="" class="searchIcon">
                <input  v-model="username" type="text" class="inputs" placeholder="Search GitHub username…" >
                <div class="noResultsDiv">
                  <p class="noResults" v-if="userNotFound">No results</p>
                  <button @click="searchUser">Search</button>
                </div>
            </div>
        </div>
    </div>
    <div class="lds-ellipsis"  v-if="loading"><div></div><div></div><div></div><div></div></div>

   <GitDetails :userData="user"/>
  </div>
</template>

<style scoped>
 
 .headSaearch{
    display: flex;
    flex-direction: column;
    gap: 36px;
 }
.header h2{
  font-size: 26px;
  font-weight: 700;
  line-height: 39px;
  text-align: left;
  color: #222731;
}

.header h5{
  font-size: 13px;
  font-weight: 700;
  line-height: 19px;
  letter-spacing: 2.5px;
  text-align: right;
  color: #4B6A9B;
}

.header{
  display: flex;
  justify-content: space-between;
}

.search{
    border-radius: 15px;
    display: flex;
    justify-content: space-between;
    background: #FEFEFE;
    box-shadow: 0px 16px 30px -10px rgba(70, 96, 187, 0.20);
    padding: 6.5px 7px;

}

.inputs{
    border: none;
}
.noResultsDiv {
  display: flex;
   gap: 5px;
   text-align: center;
   align-items: center;
} 

button{
    border: none;
    background-color: #0079FF;
    border-radius: 5px;
    padding:12.5px 18px;
    cursor: pointer;

}
.noResults{
  font-size: 12px;
  color: red;
}

.searchIcon{
    max-height: 100%;
    height: 20.04px;
    align-self: center;
}

.lds-ellipsis {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ellipsis div {
  position: absolute;
  top: 33px;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background: #fff;
  animation-timing-function: cubic-bezier(0, 1, 1, 0);
}
.lds-ellipsis div:nth-child(1) {
  left: 8px;
  animation: lds-ellipsis1 0.6s infinite;
}
.lds-ellipsis div:nth-child(2) {
  left: 8px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(3) {
  left: 32px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(4) {
  left: 56px;
  animation: lds-ellipsis3 0.6s infinite;
}
@keyframes lds-ellipsis1 {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes lds-ellipsis3 {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}
@keyframes lds-ellipsis2 {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(24px, 0);
  }
}

@media (min-width: 600px) {
  .container{
    padding: 140px 98px 236px 97px;
  }
}

@media (min-width: 1200px){
    .container{
      padding: 144px 355px;
    }
  }
</style>




