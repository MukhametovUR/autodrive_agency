<template>
  <div v-if="getBody.length == 0">
    <form @submit.prevent="postForm">
      <h2 class="contetn__title my-2 mb-10">Заказать звонок</h2>
      <div class="contetn__inputs">
        <div class="contetn__item">
          <label for="name">Имя*</label>
          <input
            id="name"
            v-model="userName"
            name="name"
            type="text"
            autocomplete="name"
            required=""
            class="appearance-none rounded-none relative block w-full my-2 px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
            placeholder="Имя"
          />{{errorName}}
        </div>
        <div class="contetn__item">
          <label for="phone">Телефон*</label>
          <input 
            id="phone"
            v-model="userPhone"
            name="phone"
            type="phone"
            autocomplete="phone"
            required=""
            class="appearance-none rounded-none relative block w-full my-2 px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
            placeholder="+7 (___) ___-__-__"
          />{{errorPhone}}
        </div>
        <div class="contetn__item">
          <label for="email">Email*</label>
          <input
            id="email-address"
            v-model="userEmail"
            type="email"
            required=""
            class="appearance-none rounded-none relative block w-full my-2 px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
            placeholder="some@some.some"
          />{{errorEmail}}

        </div>
        <div class="contetn__item">
          <label for="city">Город*</label>
          <select
            id="city"
            v-model="id"
            class="appearance-none rounded-none relative block w-full my-2 px-2 py-2 border border-gray-300 bg-white text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
          >
            <option v-for="city in cities" :key="city.id" :value="city.id">
              {{ city.name }}
            </option>
          </select>{{errorCity}}
        </div>
      </div>
      <div class="sendBtn">
        <MyButton @click="postForm" type="submit" class="m-4 bg-green-600 px-8 btn"
        >Отправить</MyButton
      >
      </div>
    </form>
  </div>
  <div v-if="getBody.length != 0" v-html="getBody" />
</template>
<script>
import axios from "axios";
import MyButton from "@/components/MyButton.vue";
import MyInput from "@/components/MyInput.vue";

export default {
  components: {
    MyButton,
    MyInput,
  },
  data() {
    return {
      userName: "",
      userPhone: "",
      userEmail: "",
      getBody: "",
      errorName:null,
      errorPhone:null,
      errorEmail:null,
      errorCity:null,
      id: null,
      cities: [
        { id: 1, name: "Москва" },
        { id: 2, name: "Санкт-Петербург" },
        { id: 3, name: "Казань" },
      ],
    };
  },

  methods: {
    postForm() {
       this.errorName =''
       this.errorPhone =''
       this.errorEmail=''
      if(!this.userName){
        this.errorName ='Обязательное поле'
      }
      if (!this.validEmail(this.userEmail)) {
        this.errorEmail ='Обязательное поле'
      }
       if (!this.validPhone(this.userPhone)) {
        this.errorPhone ='Обязательное поле'
      }
      if (
        this.userName.trim() &&
        this.userPhone.trim() &&
        this.userEmail.trim() &&
        this.id != null
      ) {
        axios
          .post(`http://hh.autodrive-agency.ru/test-tasks/front/task-7/`, {
            name: this.userName,
            phone: this.userPhone,
            email: this.userEmail,
            city_id: this.id,
          })
          .then((response) => {
            this.getBody = response.data;
          });
      }
      // (this.userName = ""),
      //   (this.userPhone = ""),
      //   (this.userEmail = ""),
      //   (this.id = "");
    },
    validEmail(userEmail) {
      let ree = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return ree.test(userEmail)
  },  
   validPhone(userPhone) {
      let rep = /^\+?[78][-\(]?\d{3}\)?-?\d{3}-?\d{2}-?\d{2}$/;
      return rep.test(userPhone)
  },  
  
  }
};
</script>
<style scoped>
.contetn__title {
  display: flex;
  font-size: 24px;
  font-weight: 500;
  line-height: 24px;
  letter-spacing: 0em;
  text-align: left;
}
.contetn__inputs {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.contetn__item {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  margin: 0 15px;
  flex-grow: 1 ;
}
.sendBtn {
  display: flex;
  justify-content: flex-end;
}
@media  (max-width:480px) {
  .btn{
    display: flex;
    justify-content: center;
    flex-grow: 1;
    align-items: center;

  }
}
</style>
