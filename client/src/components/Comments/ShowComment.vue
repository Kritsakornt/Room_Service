<template>
  <div> 
    <b-container class="bv-example-row">
      <b-row class="text-left">
        <b-col></b-col>
          <b-col cols="10" class="bg3">
            <center><h2><b><p>รายละเอียดของรายการซ่อม</p></b></h2></center>
            <hr>
            <div class="box3">
              <h4><b><p>รายการซ่อมที่ : {{ comment.id }}</p></b></h4>
              <hr>
              <p><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;หัวข้อ : </b>{{ comment.title }}</p>
              <p><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ชื่อภาพ : </b>{{ comment.thumbnail }}</p>
              <transition name="fade"> 
                <div class="thumbnail-pic" v-if="comment.thumbnail != 'null'">
                <img :src="BASE_URL+comment.thumbnail" alt="thumbnail">
                </div>
              </transition>
              <p><b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;เนื้อหา : </b>{{ comment.content }}</p>
              <hr>
              <p>
              <b-button variant="warning" v-on:click="navigateTo('/comment/edit/' + comment.id)">แก้ไขรายการ</b-button>
              <b-button variant="secondary" v-on:click="navigateTo('/comments')">ย้อนกลับ</b-button>
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
      comment: null,
    };
  },
  async created() {
    try {
      let commentId = this.$route.params.commentId;
      this.comment = (await CommentService.show(commentId)).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
  },
};
</script>
<style scoped>
</style>