<template>
  <section class="container">

    <iframe
      :src="iframeurl"
      frameborder="0"
      width="1700"
      height="900"
      allowtransparency
    ></iframe>

  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data: function(){
    return {
      iframeurl: ""
    }
  },

  mounted() {
    // you will need to install via 'npm install jsonwebtoken' or in your package.json

    var jwt = require("jsonwebtoken");

    const METABASE_SITE_URL = "http://staging.alpha.bi.onepipe.io";
    const METABASE_SECRET_KEY = "b1bd49bd5f5722b1d95fad307034494e2fa7ea4d450de66d65eca4a0ca9cad62";

    let payload = {
      resource: { dashboard: 14 },
      params: {}
    };
    let token = jwt.sign(payload, METABASE_SECRET_KEY);

    this.iframeurl = METABASE_SITE_URL + "/embed/dashboard/" + token + "#bordered=false&titled=true";
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
