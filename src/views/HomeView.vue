<template>
  <div class="container mx-auto">
    <MyButton @click="showDialog" class="m-16 bg-indigo-600">Заказать в Москву</MyButton>
    <MyButton @click="showDialog" class="m-16 bg-teal-600">Заказать в Санкт-Петербург</MyButton>
    <MyDialog v-model:show="dialogVisible">
      <PostForm/>
    </MyDialog>

  </div>
</template>

<script>
import axios from "axios";
import MyButton from "@/components/MyButton.vue";
import PostForm from "@/components/PostForm.vue";
import MyDialog from "@/components/MyDialog.vue";




export default {
  name: "HomeView",
  components: {
    MyButton,
    PostForm,
    MyDialog,
    
  },
  data(){
    return{
      dialogVisible:false,
      dialogVis:true
    }
  },
  methods: {
    showDialog(){
      this.dialogVisible=true;
    }
  }

};
</script>
