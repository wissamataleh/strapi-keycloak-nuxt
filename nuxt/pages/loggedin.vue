<template>
  <div>
    Logged in as:
    <pre>
    {{user}}
    </pre>
  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    data() {
      return {
        user: {}
      }
    },
    async fetch() {
      var config = {
        method: 'get',
        url: `http://localhost:1337/auth/keycloak/callback?access_token=${this.token}`,
      };
      await axios(config)
        .then(response => {
          console.log(response.data)
          this.user = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
    computed: {
      token() {
        return this.$route.query.access_token
      }
    },

  }

</script>
