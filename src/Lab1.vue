<script setup>
  import {ref, reactive} from 'vue';
  
  const user = reactive({
      name:"",
      surname: "",
      sex: "",
      password: ""
    });

  let confirmPassword = ref('');
  let show_info = ref(false);

  let checked_pass = ref(false);
  function sign_in(){
    console.log("Данные формы:", user);
    show_info.value = true;
    return;
  }
  function check_pass(){
    if (user.password !== confirmPassword.value){
      checked_pass.value = false;
      show_info.value = false;
    }
    else checked_pass.value = true;
  }
  
  let showpass = ref(false);
 
</script>

<template>
  <main>
    
    <div class="info">
      <h1>Регистрация</h1><br>

      <div class="data">

        <label for="name">Name</label><br>
        <input type="text" name="name" v-model="user.name"/> <br>

        <label for="surname">Surname</label><br>
        <input type="text" name="surname" v-model="user.surname"/><br>

        <div >
          <input type="radio" name="male" value="male" v-model="user.sex" checked/>
          <label for="male" class="sex">Male</label>
          <input type="radio" name="female" value="female" v-model="user.sex"/>
          <label for="female" class="sex">Female</label>
        </div>

        <label for="password">Password</label><br>
        <input @input="check_pass()" :type = 'showpass? "text":"password"' name="password" v-model="user.password"/>

        <input @mousedown="showpass=true" @mouseup="showpass=false" 
               type="button" name="show" value="show" ><br>

        <label for="confirmPassword">Confirm Password</label><br>
        <input @input="check_pass()" :type = 'showpass? "text":"password"' name="confirmPassword " v-model="confirmPassword "/><br>
        
      </div>

    <input @click="sign_in()" type="button" id="sign_in" :disabled="!checked_pass" value="Sign In"/>
    
    <p v-if="show_info">
          Пользователь: {{ user.name }} {{ user.surname }}. {{ user.sex === 'male' ? 'Мужского' : 'Женского' }} пола.
        </p>

    </div>
    
    

  </main>
  
</template>

<style scoped>
  input{
    margin-bottom: 10px;
  }
  
  .info{
    padding: 40px;
    margin: 30px;
    height: 500px;
    width: 300px;
    border: 2px;
    border-color: cadetblue;
    border-style: dashed;
    
  }

  .sex{
    margin-right:40px;
  }
  .show{
    margin-left:10px;
  }
  #sign_in{
    width:80%;
    height: 30px;
  }
</style>
