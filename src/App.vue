<template>
  <div class="container">
    <div class="logo"><img src="./assets/logo.svg" alt=""></div>
    <input-container></input-container>
  </div>
</template>

<script>
import InputContainer from './components/InputContainer.vue'

export default {
  components: {
    InputContainer,
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  height: 100vh;
  width: 100%;
  font-family: 'Space Mono';
  background-color: #C5E4E7;
}

.logo {
  text-align: center;
  margin-top: 1.7rem;
  margin-bottom: 2.3rem;
}


.bill, .result {
background-color: white;
display: flex;
flex-direction: column;
padding: 2rem; 
border-radius: 1.4rem 1.4rem 0 0;
}

label {
  color: #5E7A7D;
  font-weight: 700;
  margin-bottom: 0.3rem;
}

input {
  border: none;
  outline: none;
  padding: 5px;
  padding-right: 10px;
  background-position: 17px 15px;
  background-repeat: no-repeat;
  background-color: #F3F9FA;
  text-align: right;
  font-size: 24px;
  color: #547878;
  font-weight: bolder;
  font-family: 'Space Mono';

  
}

input[type=number] {
  appearance: textfield;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

@media only screen and (min-width: 1000px) {
    body {
      display: flex;
      flex-direction: column;
      align-items: center;  
    }
}



 

</style>
