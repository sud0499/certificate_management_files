<template>
  <NavBar />
  <div class="public">
    <div id="public_text">
      <h1>
        Welcome to Public Verify Certificate,
        <h6>
          ------------------------------------------------------------------------------
        </h6>
        Validate Your Certificates Here
      </h1>
    </div>
    <div id="public_search">
      <div class="search">
        <h2>Verify Certificates Here</h2>
        <div>
          <input
            id="CertificateId"
            type="text"
            placeholder="Enter Certificate id"
            name="cert_id"
            v-model="certId"
            required
          />
        </div>
        <div id="btn">
          <button v-on:click="search()" id="submit" type="submit">
            Verify
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from "../components/NavBar.vue";
import axios from "axios";
export default {
  name: "PublicPage",
  components: {
    NavBar,
  },
  data() {
    return {
      certId: "",
    };
  },
  methods: {
    async search() {
      let result = await axios.get(
        `http://localhost:4000/certs/${this.certId}`
      );
      if (result.status == 200) {
        localStorage.clear();
        localStorage.setItem("certId", result.data.cert[0]._id);
        this.$router.push("/verify");
      }
      if (result.status == 204) {
        alert(result.statusText);
      }
    },
  },
};
</script>
<style scoped>
.public {
  height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
#public_text,
#public_search {
  width: 50vw;
  display: flex;
  justify-content: center;
  align-items: center;
}
h1 {
  color: rgb(120, 70, 70);
}
</style>
