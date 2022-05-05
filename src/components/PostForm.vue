<template>
  <div>
    <form @submit.prevent="postForm">
      <h2 class="contetn__title">Заказать звонок</h2>
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
          />
        </div>
        <div class="contetn__item">
          <label for="phone">Телефон*</label>
          <input
            id="phone"
            v-model="userPhone"
            data-mask="+7 (___) ___-__-__"
            name="phone"
            type="phone"
            autocomplete="phone"
            required=""
            class="appearance-none rounded-none relative block w-full my-2 px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
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
            class="appearance-none rounded-none relative block w-full my-2 px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
            placeholder="some@some.some"
          />
        </div>
        <div class="contetn__item">
          <label for="city">Город*</label>

          <select
            id="city"
            v-model="id"
            class="appearance-none rounded-none relative block w-full px-1 py-2 border border-gray-300 placeholder-white-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
          >
            <option v-for="city in cities" :key="city.id" :value="city.id">
              {{ city.name }}
            </option>
          </select>
        </div>
      </div>

      <MyButton @click="postForm" type="submit" class="m-4 bg-green-600"
        >Отправить</MyButton
      >
    </form>
    <div v-html="getBody" />
  </div>
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
      console.log(
        "name: " + this.userName,
        "phone: " + this.userPhone,
        "email: " + this.userEmail,
        "city_id: " + this.id
      );
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
            console.log(this.getBody);
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
}
.contetn__item {
  flex-direction: column;
}
</style>
