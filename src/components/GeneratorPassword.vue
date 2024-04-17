<template>
  <div class="password-generator-container">
    <h2 class="password-generator-title">Gerador de Senhas</h2>
    <label for="length">Tamanho da Senha</label>
    <input type="number" id="length" v-model="passwordLength" min="4" max="32">
    <br>

    <div class="container">
      <div class="checkboxs">
        <label for="includeUppercase"> Letras Maiúsculas: </label>
        <input type="checkbox" id="includeUppercase" v-model="includeUppercase">
      </div>
  
      <div class="checkboxs">
        <label for="includeNumbers">Números: </label>
        <input type="checkbox" id="includeNumbers" v-model="includeNumbers">
      </div>
      
      <div class="checkboxs">
        <label for="includeSymbols">Símbolos: </label>
        <input type="checkbox" id="includeSymbols" v-model="includeSymbols">
      </div>



    </div>


    <button @click="generatePassword" class="generatedPassword-button">Gerar Senha</button>

    <div v-if="generatePassword" class="generated-password">
      <strong>Sua Senha: </strong> {{  generatedPassword }}
    </div>
  </div>

</template>

<script setup>
import { ref } from "vue";

const passwordLength = ref(12);
const includeUppercase = ref(true);
const includeNumbers = ref(true);
const includeSymbols = ref(true);
const generatedPassword = ref("");

const generatePassword = () => {
  const lowercase = "abcdefghijklmnopqrstuvwxyz";
  const uppercase = includeUppercase.value ? "ABCDEFGHIJKLMNOPQRSTUVWXYZ" : "";
  const numbers = includeNumbers.value ? "0123456789" : "";
  const symbols = includeNumbers.value ? "!@#$%^&*()_+[]{}|;:,.<>?/~`" : "";

  let password = "";

  const all = lowercase + uppercase + numbers + symbols;
  for (let i = 0; i < passwordLength.value; i++){
    const randomIndex = Math.floor(Math.random() * all.length);
    password += all[randomIndex];
  }

  generatedPassword.value = password;
};
</script>

<style scoped>

.password-generator-container{
  max-width: 400px;
  margin: 50px auto;
}
.password-generator-title{
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;

}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  
}

.generate-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}


.generatedPassword-button{
  background-color: #949494;
  border-radius: 4px;
}

.generatedPassword-button:hover{
  background-color: #c2c2c2;
}


.generated-password{
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #f9f9f9;
  color: #333;
}

.container {
  display: flex;
  justify-content: space-between;
  flex-direction: row;
}

</style>
