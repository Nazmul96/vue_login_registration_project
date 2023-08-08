<script setup>
  import { ref, reactive, computed } from 'vue';
  let error_message = ref('');
  let login_form = ref(true);
  let registration_form = ref(false);
  let successful_login = ref(false);
  let message = ref('');

  const login_info =reactive({
    user_name:'',password:''
  });

  const registration_info = reactive({
      user_name:'',password:'',confirm_password:''
  });

  const user_info = [
    {user_name:'nazmul',password:'1234'}
  ]
  function userLogin(){
      if((login_info.user_name == '') || (login_info.password == '')){

          error_message.value = "user name and password must be required";
      }
      else{
        user_info.forEach(function(user){
          if((user.user_name == login_info.user_name)&&(user.password == login_info.password)){
              login_form.value  = false;
              successful_login.value  = true;
              message.value = 'successfully logged in';
          }
          else{
              error_message.value = "your credential do not match";
          }
        });
      }
  }

  function backLoginPage(){
     login_info.user_name='';
     login_info.password='';

     error_message.value = '';
     successful_login.value  = false;
     login_form.value = true;
  }

  function userRegistration(){
      registration_form.value = true;
      login_form.value = false;
  }
 
  function Registration(){
    if((registration_info.user_name == '') || (registration_info.password == '') || (registration_info.confrim_password == '')){
        error_message.value = "user name,password and confirm password must be required";
    }
    else{
        user_info.forEach(function(user){
          if(registration_info.password != registration_info.confirm_password){
                error_message.value = "Password and confirm password do not matched";
          }
          else{
              console.log(registration_info);
              user_info.push(registration_info); 
              registration_form.value  = false;
              successful_login.value  = true;
              message.value = 'successfully Registered'
          }
        });
    }
  }
</script>

<template>
  <section class="flex h-screen w-full">
    <div class="w-1/2" style="background-image: url(https://images.unsplash.com/photo-1690555575753-7aa27df96b52?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80); background-repeat: no-repeat; background-size: cover;">
      <h1 class="mb-5 text-2xl mt-10 ml-10 text-white">Kosmos!</h1>
    </div>
    <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200 mb-5" v-show="login_form">
      <h2 class="mb-5 text-xl">Login or register</h2>
      <div class="w-full max-w-xs">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
          <p style="color: brown;">{{ error_message }}</p>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Username
            </label>
            <p>{{ login_info }}</p>
            <p>{{ user_info }}</p>
            <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Username" v-model="login_info.user_name">
          </div>
          <div class="mb-6">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
              Password
            </label>
            <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" placeholder="******************" v-model="login_info.password">

          </div>
    
          <div class="flex items-center justify-between">
            <button class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button" @click="userLogin()">
              Sign In
            </button>
            <button type="button" class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" @click="userRegistration()">
              Or Register
            </button>
          </div>

        </form>
        <p class="text-center text-gray-500 text-xs">
          &copy;2020 Acme Corp. All rights reserved.
        </p>
      </div>
    </div>
<!-- Registration form-->
    <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200 mb-5" v-show="registration_form">
      <h2 class="mb-5 text-xl">register</h2>
      <div class="w-full max-w-xs">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
          <p style="color: brown;">{{ error_message }}</p>
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
              Username
            </label>
            <p>{{ registration_info }}</p>
            <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Username" v-model="registration_info.user_name">
          </div>
          <div class="mb-6">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
              Password
            </label>
            <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" placeholder="******************" v-model="registration_info.password">

          </div>
    

          <div class="mb-6">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="confirm_password">
                Confirm Password
              </label>
              <input class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="confirm_password" type="password" placeholder="******************" v-model="registration_info.confirm_password">
          </div>

    
          <div class="flex items-center justify-between">
            <button type="button" class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" @click="Registration()">
              Register
            </button>
          </div>

        </form>
        <p class="text-center text-gray-500 text-xs">
          &copy;2020 Acme Corp. All rights reserved.
        </p>
      </div>
    </div>
    <!-- after login show success message-->
    <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200" v-show="successful_login">
      <p>{{ user_info }}</p>
          <h4 style="color:green">{{ message }}</h4>
          <button class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button" @click="backLoginPage()">
             Back
            </button>
    </div>

  </section>
</template>
<style scoped></style>
