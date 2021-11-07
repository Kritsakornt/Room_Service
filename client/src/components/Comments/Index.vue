<template>
  <div>
    <b-container class="bv-example-row">
    <b-row class="text-left">
         <b-col></b-col>
         <b-col cols="10" class="bg3">
          <center>
            <h1><b>Notify Repair</b></h1>
            <h5>จำนวนรายการที่ต้องซ่อม {{ comments.length }} รายการ</h5>
            <hr>
          </center>
          <div class="d-grid gap-2 col-6 mx-auto">
            <b-button variant="success" v-on:click="navigateTo('/comment/create')">สร้างรายการ</b-button>
          </div>
          <br>
          <div  class="box3" v-for="comment in comments" v-bind:key="comment.id">
            <h4><b><p>รายการซ่อมที่ : {{ comment.id }}</p></b></h4>
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>หัวข้อ : </b>{{ comment.title }}</p>
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>ชื่อภาพ : </b>{{ comment.thumbnail }}</p>
            <transition name="fade"> 
              <div class="thumbnail-pic" v-if="comment.thumbnail != 'null'">
                <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img :src="BASE_URL+comment.thumbnail" alt="thumbnail"></p>
              </div>
            </transition>
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>เนื้อหา : </b>{{ comment.content }}</p>
            <hr>
            <p>
              <b-button variant="primary" v-on:click="navigateTo('comment/'+comment.id)"> ดูรายละเอียด </b-button>
              <b-button variant="warning" v-on:click="navigateTo('/comment/edit/' +comment.id)"> แก้ไขรายการ </b-button>
              <b-button variant="danger" v-on:click="deleteComment(comment)"> ลบรายการนี้ </b-button>
            </p>
          </div>
        </b-col>
      <b-col> </b-col>
     </b-row>
  </b-container>
  </div>
</template>
<script>
import CommentService from "@/services/CommentsService";
export default {
  data() {
    return {
         BASE_URL: "http://localhost:8081/assets/uploads/",
      comments: [],
    };
  },
  async created() {
    this.comments = (await CommentService.index()).data;
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteComment(comment) {
      let result = confirm("คุณแน่ใจนะ ที่จะลบรายการนี้?");
      if (result) {
        try {
          await CommentService.delete(comment);
          this.refreshData();
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      this.comments = (await CommentService.index()).data;
    },
  },
};
</script>
<style scoped>
</style>