<script setup>
// import { normalizeClass } from 'vue';
// import { ref } from 'vue';
// import axios from 'axios';
// makes browsers render all elements more consistently and in line with modern standards. It precisely targets only the styles that need normalizing.
import moment from "moment";
import { ref } from "vue";

const props = defineProps({
  userData: Object,})

//  defineProps(['Image','profileName','link','date','BIO','public_repos', 'followers', 'following','location','attacheee','twitter','buildinng'])
//  import attacheee from ;
//  import location from '@/assets/location.svg';
//  import officeBuilding from '@/assets/officeBuilding.png';
//  import twitter from '@/assets/twitter.png';

const username = ref("")
const user = ref (null)
const userNotFound = ref(false);
const loading = ref(false)
</script>

<template>
<div class="detailsContainer" v-if="userData">
    <div class="firstDiv">
        <img :src="userData?.avatar_url" alt="No Image" class="avatartImg">
        <div>
            <h3>{{ userData?.name}}</h3>
            <p>{{ userData?.link }}</p>
            <p>Joined {{moment(userData?.create_at).format("D MMM YYYY") }}</p>
        </div>
    </div>
    <div class="BIO">
        <p>{{ userData?.BIO || "No bio found"}}</p>
    </div>
    <div class="repoContainer">
        <div class="repo">
            <p>Repos</p>
            <p>{{ userData?.public_repos }}</p>
        </div>
        <div class="followers">
            <p>Followers</p>
            <p>{{ userData?.followers }}</p>     
        </div>
        <div class="following">
             <p>Following</p>  
            <p>{{userData?.following }}</p>
        </div>
    </div>
   
    <div class="imgtexts">
        <div class="location">
            <img src="@/assets/location.svg" alt="">
            <p>{{ userData?.location ||'Not Available'  }}</p>
        </div>
        <div class="attacheee">
            <img src="@/assets/attacheee.png" alt="">
            <p>{{ userData?.url  }}</p>
        </div>
        <div class="twitter">
            <img src="@/assets/officeBuilding.png" alt="">
             <p>{{ userData?.twitter_username ||'Not Available'}}</p>
        </div>
        <div class="buildinng">
            <img src="@/assets/twitter.png" alt="">
            <p>{{ userData?.twitter_username||'Not Available' }}</p>
        </div>
    </div>
</div>
</template>

<style scoped>
.firstDiv{
    display: flex;
  gap: 20px;
  align-items: center;
}
.detailsContainer{
    background-color: #FEFEFE;
    margin-top: 16px;
    border-radius: 10px;
    padding: 32px 24px 48px 24px;
    display: flex;
    flex-direction: column;
    gap: 30px;
}
.repoContainer{
    display: flex;
    justify-content: space-evenly;
    padding:18px 14px 19px 15px;
    background-color: #f6f8ff;
    border-radius:10px ;
}

h3,
h4,
p {
  color: #222731;
font-size: 12px;
font-weight: 400;
line-height: 22px;

}

.avatartImg{
    max-width: 70px;
    width: 100%;
    max-height: 70px;
    height: 100%;
/* top: 32px
left: 24px */

}

.repo{
    display: flex;
    flex-direction: column;
}

.followers{
    display: flex;
    flex-direction: column;
}

.following{
    display: flex;
    flex-direction: column;
}

.imgtexts{
display: flex;
flex-direction: column;
gap: 16px;
}

.location{
display: flex;
}

.attacheee{
    display: flex;
}

.twitter{
    display: flex;
}

.buildinng{
    display: flex; 
}


@media (min-width: 600px){
    .imgtexts{
        display: grid;
        grid-template-columns: 1fr 1fr;
    }
    
}
</style>
