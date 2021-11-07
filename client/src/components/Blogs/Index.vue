<template>
  <div>
    <b-container class="bv-example-row">
      <div class="" >
        <b-row class="text-left">
        <b-col></b-col>
          <b-col cols="10" class="bg1">
            <center>
            <h1><b>Room Service</b></h1>
            <h5>จำนวนที่จองที่มี {{ blogs.length }} คิว</h5></center>
            <hr>
            <div class="d-grid gap-2 col-6 mx-auto">
                <b-button variant="btn btn-success" v-on:click="navigateTo('/blog/create')"> จองหอพัก </b-button>
            </div>

            <br>
            <div class="box1" v-for="blog in blogs" v-bind:key="blog.id">
              <h4><b><p>คิวที่ : {{ blog.id }}</p></b></h4>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>ชื่อ - นามสกุล :</b> {{ blog.firstname }}  {{ blog.lastname }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>จำนวนคนเข้าพัก :</b> {{ blog.pnum }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>ลักษณะห้องพัก :</b> {{ blog.nroom }}</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>เบอร์โทรศัพท์ :</b> {{ blog.tel }}</p>
              <hr>
              <p>
                <b-button variant="primary" v-on:click="navigateTo('blog/'+blog.id)"> ตรวจสอบข้อมูล </b-button>
                <b-button variant="danger" v-on:click="deleteBlog(blog)"> ยกเลิกการจอง</b-button> 
              </p> 
            </div>
    
          </b-col>
        <b-col></b-col>
        </b-row>
      </div>
    </b-container>
  </div>
</template>
<script>
import BlogService from "@/services/BlogsService";
export default {
  data() {
    return {
      blogs: [],
    };
  },
  async created() {
    this.blogs = (await BlogService.index()).data;
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteBlog(blog) {
      let result = confirm("ต้องการยกเลิกการจองหอพักนี้ ?");
      if (result) {
        try {
          await BlogService.delete(blog);
          this.refreshData();
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      this.blogs = (await BlogService.index()).data;
    },
  },
};
</script>
<style scoped>

</style>