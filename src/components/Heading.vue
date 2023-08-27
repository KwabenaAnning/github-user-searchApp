<script>
defineProps
</script>


<template>
    <div class="container" >
      <header>
          <h2>devfinder</h2>
          <h5>Dark</h5>
      </header>
      <div class="searchPlace">
         <input type="text" placeholder="Search GitHub username..">
         <button>Search</button>
       </div>
       <main>
        <img src="" alt="">
        <div class="Octat">

          
        </div>
       </main>
    </div>
  </template>
  
  <style scoped>
   
  .header h2{
    font-size: 26px;
    font-weight: 700;
    line-height: 39px;
    text-align: center;
    background: #222731;
  }
  
  .header h5{
    font-size: 13px;
    font-weight: 700;
    line-height: 19px;
    letter-spacing: 2.5px;
    text-align: center;
    background: #4B6A9B;
    align-items: center;
  }
  
  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .container{
    background: #F6F8FF;
  }

  .searchPlace{
    border-radius: 5px;

  }
  </style>


<!-- <script>

</script>

<template>

<p> devfinder</p>
<span> LIGHT</span>


</template>

<style>

</style> -->