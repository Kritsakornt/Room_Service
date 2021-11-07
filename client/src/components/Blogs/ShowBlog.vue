<template>
  <div>
    <b-container class="bv-example-row">
      <b-row class="text-left">
        <b-col></b-col>
        <b-col cols="10" class="bg1">
        <center>
          <h1><b>Room Service</b></h1>
          <h5>รายละเอียดการจองที่ {{ blog.id }} </h5><hr>
        </center>
        <div class="box1">
              <h4><b><p>คิวที่ : {{ blog.id }}</p></b></h4>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>ชื่อ - นามสกุล</b> : {{ blog.firstname }}  {{ blog.lastname }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>เบอร์โทรศัพท์</b> : {{ blog.tel }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>ลักษณะห้องพัก</b> : {{ blog.nroom }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>จำนวนคนเข้าพัก</b> : {{ blog.pnum }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>วันที่ Check in</b> : {{ blog.dates }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>วันที่ Check out</b> : {{ blog.datee }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>เวลาที่ Check in</b> : {{ blog.times }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>เวลาที่ Check out</b> : {{ blog.timee }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>บริการอื่นๆ</b> : {{ blog.other }}</p>
              <hr>
            <p>
              <b-button variant="warning" v-on:click="navigateTo('/blog/edit/' + blog.id)">
                แก้ไขการจอง
              </b-button>
              <b-button variant="secondary" v-on:click="navigateTo('/blogs')">ย้อนกลับ</b-button>
            </p>
        </div>
        </b-col>
        <b-col></b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import BlogService from "@/services/BlogsService";
export default {
  data() {
    return {
      blog: null,
    };
  },
  async created() {
    try {
      let blogId = this.$route.params.blogId;
      this.blog = (await BlogService.show(blogId)).data;
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