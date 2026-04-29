
  <script setup>
  import { ref } from 'vue';
  
  let stickerURL = ref(null);
  const loading = ref(false);
  const api_key = 'c5EULzdKb6V42UcW6EHPwavB0lXIOoRT'
  async function fetchSticker (){
    loading.value = true
    try{
      
      const response = await fetch(`https://api.giphy.com/v1/stickers/random?api_key=${api_key}`)
      const data = await response.json()
      console.log(data)
      stickerURL.value = data.data.images.original.url
    }catch(error){
      console.error(error)
    }finally{
      loading.value=false
    }
    
  }
  
  </script>
  
  <template>
    <div class="app">
      <h1>Random Sticker Generator</h1>
      <p>Click the button below to generate a random sticker:</p>
      <div class="sticker-container" v-if="stickerURL">
        <img :src="stickerURL" alt="Random Sticker">
      </div>
      <div class="sticker-container" v-else>
        <p>Press the button to get sticker</p>
      </div>
      <button @click="fetchSticker" :disabled="loading">{{ loading ? 'Loading..' :'Get Sticker'}}</button>
    </div>
  </template>
  
  <style>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body{
    background: linear-gradient(135deg,#667eea 0%,#764ba2 100%);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  .app{

    text-align: center;
    padding: 40px;
    background: white;
    border-radius: 30px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.3);
    max-width: 600px;
   margin: 20px auto;
  }
  h1{
    color :#333;
    margin-bottom: 30px;
    font-size: 2rem;
  }
  .sticker-container {
    margin: 30px auto;
    min-height: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #f8f9fa;
    border-radius: 20px;
    padding: 20px;
  }
  .sticker-container img {
    max-width: 280px;
    max-height: 280px;
    border-radius: 20px;
    box-shadow: 0 8px 25px rgba(0,0,0,0.15);
  
  }
  .sticker-container p{
    color :#999;
    font-size: 1.2rem;
  }
  button{
    background: linear-gradient(135deg,#667eea 0%,#764ba2 100%);
    color : white;
    border: none;
    padding: 15px 35px;
    font-size: 1.2rem;
    font-weight: bold;
    border-radius: 50px;
    cursor: pointer;
    transition: transform 0.2s,box-shadow 0.2s ;
    margin-top: 10px;
  }
  button:hover{
    transform: scale(1.05);
    box-shadow: 0 10px 25px rgba(0,0,0,0.2);
  }
  button:disabled{
    opacity: 0.6;
    transform: none;
    cursor: not-allowed;
  }
  </style>
  