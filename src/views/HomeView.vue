<template>
  <div class="container mx-auto">
    <MyButton @click="showDialog" class="m-16 bg-indigo-600">Заказать в Москву</MyButton>
    <MyButton @click="showDialog" class="m-16 bg-teal-600" >Заказать в Санкт-Петербург</MyButton>
    <MyDialog v-model:show="dialogVisible">
          <a class="close" href="#" @click="closeDialog">&times;</a>
      <PostForm/>
    </MyDialog>

  </div>
</template>

<script>
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
      idCity:null
    }
  },
  methods: {
    showDialog(event){
      this.dialogVisible=true;
      if(event.target.text=="Заказать в Москву")
      this.idCity = 1;
      if(event.target.text=="Заказать в Санкт-Петербург")
      this.idCity = 2;
    },
    closeDialog(){
      this.dialogVisible=false;
    }
  }

};
</script>
<style scoped>
.close{
  display: flex;
  justify-content: flex-end;
  right: 0;
  transition: all 200ms;
  font-size: 30px;
  font-weight: bold;
  text-decoration: none;
  color: #333;
}
</style>
