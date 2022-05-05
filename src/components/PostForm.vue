<template>
  <div v-if="getBody.length == 0">
    <form @submit.prevent="postForm">
      <h2 class="contetn__title my-4 py-3 mb-10">Заказать звонок</h2>
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
            class="appearance-none rounded-none relative block w-full ml-8 my-2 px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
            placeholder="Имя"
          />
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
            class="appearance-none rounded-none relative block w-full ml-8 my-2 px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
            placeholder="+7 (___) ___-__-__"
          />
        </div>
        <div class="contetn__item">
          <label for="email">Email*</label>
          <input
            id="email-address"
            v-model="userEmail"
            type="email"
            autocomplete="email"
            required=""
            class="appearance-none rounded-none relative block w-full ml-8 my-2 px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
            placeholder="some@some.some"
          />
        </div>
        <div class="contetn__item">
          <label for="city">Город*</label>

          <select
            id="city"
            v-model="id"
            class="appearance-none rounded-none relative block w-full my-2 ml-8 px-2 py-2 border border-gray-300 bg-white text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
          >
            <option v-for="city in cities" :key="city.id" :value="city.id">
              {{ city.name }}
            </option>
          </select>
        </div>
      </div>
      <MyButton @click="postForm" type="submit" class="m-4 bg-green-600 btn"
        >Отправить</MyButton
      >
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
      (this.userName = ""),
        (this.userPhone = ""),
        (this.userEmail = ""),
        (this.id = "");
    },
  },
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
  justify-content: center;
}
.contetn__item {
  flex-direction: column;
}
.btn {
  right: 0;
}
</style>
