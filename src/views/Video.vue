<template>
  <div class="Header">
    <div class="Home-Header">VIDEO PACHA TV</div>
    <router-link to="/videos">
      <div class="Agregar-Header">Ver Mapa</div>
    </router-link>
  </div>
  <div class="Detalle-Texto">Fortnite</div>
  <video src="{{video.url}}" class="Detalle-Video"></video>
  <p class="Tittle-Detalle">{{ video.title }}</p>
  <p class="Desc-Detalle">{{ video.desc }}</p>
</template>

<script>
export default {
  data() {
    return {
      video: {},
    };
  },

  methods: {
    async getVideo() {
      const info = await fetch(
        `http://localhost:3000/movies/${this.$route.params.id}`
      );
      const data = await info.json();
      this.video = data;
      console.log(data);
    },
  },

  created() {
    this.getVideo();
  },
};
</script>

<style>
body {
  margin: 0%;
}

.Header {
  height: 74px;
  margin: 0%;
  padding: 0;
  background-color: #ff5252;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.Home-Header {
  margin-left: 20px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-weight: 700;
  font-size: 36px;
}

.Agregar-Header {
  margin-right: 20px;
}

.Detalle-Texto {
  width: 333px;
  height: 18px;
  margin-left: 21%;

  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 28px;
  line-height: 18px;
}

.Detalle-Video {
  margin: 0 auto;
  width: 1070px;
  height: 496.44px;
}

.Tittle-Detalle {
  margin: 0 auto;
  width: 1070px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 16px;
}

.Desc-Detalle {
  margin: 0 auto;
  width: 1070px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 18px;
}
</style>