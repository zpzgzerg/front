<script>
import axios from "axios";
export default {
  data() {
    return {
      response: ''
    }
  },
  methods: {
    accessTokenExpired() {
      this.axiosCall('http://localhost:8080/app1/accessfail');
    },
    refreshTokenExpired() {
      this.axiosCall('http://localhost:8080/app1/refreshfail');
    },
    resellerCall() {
      this.axiosCall('http://localhost:8080/app1/check');
    },
    openMarketCall() {
      this.axiosCall('http://localhost:8080/app2/check');
    },
    authServerCall() {
      this.axiosCall('http://localhost:8080/auth/check');
    },
    axiosCall(url) {
      axios.get(url, {}, {withCredentials: true})
          .then(res => {
            this.response = JSON.stringify(res.data);
          })
          .catch(error => {
            this.response = error;
          })
    }
  }
}
</script>


<template>
  <header>
    <div class="wrapper">
      <div>
        <button @click="accessTokenExpired">엑세스 토큰만료</button>
        <button @click="refreshTokenExpired">리프레시 토큰만료</button>
        <br/>
        <button @click="resellerCall">리셀러 호출</button>
        <button @click="openMarketCall">오픈마켓 호출</button>
        <button @click="authServerCall">인증서버 호출</button>
      </div>
    </div>
  </header>

  <main>
    <div>
      <p>응답결과</p>
      <div>
        {{response}}
      </div>
    </div>
  </main>
</template>

<style scoped>
  header {
    line-height: 1.5;
  }

  @media (min-width: 1024px) {
    header {
      display: flex;
      place-items: center;
      padding-right: calc(var(--section-gap) / 2);
    }

    header .wrapper {
      display: flex;
      place-items: flex-start;
      flex-wrap: wrap;
    }
  }
</style>
