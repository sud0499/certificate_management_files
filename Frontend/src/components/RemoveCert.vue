<template>
<LoginNavBar/>
  <div class=cert>
    <div id="ftr"><NavFeature /></div>
    <div class="form">
        <div><input type="text" placeholder="Roll No" v-model="rollNo"></div>
        <div><button v-on:click="delCert()">Delete</button></div>
    </div>   
  </div>
</template>
<script>
import LoginNavBar from './LoginNavBar.vue'
import NavFeature from './NavFeature.vue'
import axios from "axios";
export default {
    name:'RemoveCert',
    components:{
        LoginNavBar,
        NavFeature
    },
    data() {
    return {
      rollNo:"",
    };
  },
  methods: {
    async delCert() {
      let result = await axios.delete(`http://localhost:4000/certs/${this.rollNo}`);
      if (result.status == 200) {
        alert("Certificate Deleted");
      }
      localStorage.setItem("user-info",JSON.stringify(result.data))
      this.$router.push({name:'AddCert'})
    },
  },
}
</script>
<style scoped>
.cert{
  display: flex;
  height: 90vh;
}
#ftr{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-grow: 0.8;
}
.form{
  padding: 9%;
  margin-top: 8%;
}
</style>