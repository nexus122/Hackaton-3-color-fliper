<script setup>
</script>

<script>
export default {
  data() {
    return {
      color: "#61D165",
    };
  },
  methods: {
    changeColor() {
      this.color = this.colorHEX();
    },
    generarLetra() {
      var letras = ["a","b","c","d","e","f","0","1","2","3","4","5","6","7","8","9"];
      var numero = (Math.random() * 15).toFixed(0);
      return letras[numero];
    },
    colorHEX() {
      var coolor = "";
      for (var i = 0; i < 6; i++) {
        coolor = coolor + this.generarLetra();
      }
      return "#" + coolor;
    },
    copyColor(){
      // Se tiene que crear un textarea para poder copiar el color.
      var color = this.$refs.copyText.innerText;
      const el = document.createElement('textarea');  

        el.value = color;                                         
        el.setAttribute('readonly', '');                
        el.style.position = 'absolute';
        el.style.visibility = 'none';

        document.body.appendChild(el);      

        const selected =  document.getSelection().rangeCount > 0  ? document.getSelection().getRangeAt(0) : false;    

        el.select();                     

        document.execCommand('copy');                   
        document.body.removeChild(el);   

        if (selected) {                                 
          document.getSelection().removeAllRanges();    
          document.getSelection().addRange(selected);   
        }

    }
  },
};
</script>

<template>
  <main :style="{ background: color }">
    <!-- Color Fliper -->
    <h1 ref="copyText" @click="copyColor">{{ color }}</h1>
    <p>Press the button bellow to generate new colors</p>
    <button @click="changeColor">Generate Colors</button>
  </main>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");

body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  font-family: "Roboto";
  font-style: normal;
}

h1 {
  font-size: 100px;
  line-height: 24px;
  cursor:pointer;
}

p {
  font-size: 20px;
  line-height: 24px;
  font-weight: bold;
}

button {
  width: 482px;
  border-radius: 5px;
  height: 56px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
</style>
