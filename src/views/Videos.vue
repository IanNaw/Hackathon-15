<template>
  <div class="Header">
    <div class="Home-Header">VIDEO PACHA TV</div>
    <div @click="openModal" class="Agregar-Header">Agregar Video</div>
  </div>
  <div class="Texto">Lista de Videos</div>
  <div class="Grid-Container">
    <div v-for="(video, index) in videos" :key="index" class="item">
      <!-- <router-link to="/videos"></router-link> -->
      <button :data-id="video.id" @click.prevent="delData" ref="thebutton">
        x
      </button>

      <video class="video" src="{{video.url}}"></video>
      <div class="Titulo-Item">{{ video.title }}</div>
      <div class="Desc-Item">{{ video.desc }}</div>

      <router-link :to="`/videos/${video.id}`" class="Button-Center-Container">
        <button class="Detail-Button">Ver Detalle</button>
      </router-link>
    </div>
  </div>

  <div class="modal">
    <div class="modal-content">
      <div class="form">
        <h1 class="Tittle-Form">Agregar Video</h1>
        <div class="Input-Container">
          <input
            type="text"
            class="Input-Form"
            id="Titulo"
            placeholder="Titulo"
            v-model="info.title"
          />
          <input
            type="text"
            class="Input-Form"
            id="Video"
            placeholder="Url-video"
            v-model="info.url"
          />
          <input
            type="text"
            class="Input-Form"
            id="desc"
            placeholder="Descripcion"
            v-model="info.desc"
          />
        </div>
        <div class="Buttons-Container">
          <router-link to="/videos"
            ><button @click="postData" class="Agregar-Boton">
              Agregar
            </button></router-link
          >
          <button @click="closeModal" class="close Cancel-Button">
            Cancelar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      videos: [],
      info: {},
      tempId: "",
    };
  },

  methods: {
    async getVideo() {
      const info = await fetch("http://localhost:3000/movies/");
      const data = await info.json();

      this.videos = data;
      console.log(data);
    },
    openModal() {
      document.querySelector(".modal").style.display = "block";
    },
    closeModal() {
      document.querySelector(".modal").style.display = "none";
    },
    async postData() {
      console.log(JSON.stringify(this.info));
      const post = await fetch("http://localhost:3000/movies/", {
        method: "POST",
        body: JSON.stringify(this.info),
        headers: {
          "Content-Type": "application/json",
        },
      });
    },

    delData: async function (element) {
      const id = element.target.getAttribute("data-id");
      console.log(id);
      const post = await fetch(`http://localhost:3000/movies/${id}`, {
        method: "DELETE",
        headers: {
          "Content-type": "application/json",
        },
      });
      element.target.parentElement.remove();
    },
  },

  created() {
    this.getVideo();
  },
};
</script>

<style scoped>
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

.Items-Container {
  display: none;
}

.Texto {
  margin-top: 1%;
  margin-bottom: 1%;
  margin-left: 21.65%;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 28px;
}

.Grid-Container {
  margin: 0 auto;
  display: grid;
  column-gap: 1%;
  grid-template-columns: repeat(4, 255px);
  width: 1086px;
  row-gap: 1%;
}

.item {
  background: #ffffff;
  border: 1px solid #cfcfcf;
  height: 440px;
}

.video {
  width: 255px;
  height: 190px;
}

.Titulo-Item {
  margin-left: 8px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
}

.Desc-Item {
  margin-left: 8px;
  width: 226px;
  height: 93px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
}

.Button-Center-Container {
  display: flex;
  justify-content: center;
}

.Detail-Button {
  margin-top: 90px;
  width: 225px;
  height: 34px;
  background: #00c1aa;
}
</style>

<style>
.modal {
  display: none;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
}

/* Modal Content/Box */
.modal-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}

/* The Close Button */
.close {
  /* color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold; */
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>

<style>
.form {
  margin: 0 auto;

  width: 625px;
  height: 362px;
}

.Tittle-Form {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 22px;
  line-height: 26px;
}

#desc {
  background: #ffffff;
  border: 1px solid #00c1aa;
  width: 590px;
  height: 137px;
  grid-column: 1 / 3;
  grid-row: 2 / 5;
}

#Titulo {
  grid-column: 1 / 2;
  grid-row: 1 / 2;
}

#Video {
  grid-column: 2 / 3;
  grid-row: 1 / 2;
}

.Input-Container {
  row-gap: 20px;
  column-gap: 20px;
  display: grid;
  grid-template-columns: repeat(2, 287px);
  grid-template-rows: repeat(4, 42px);
}

.Input-Form {
  background: #ffffff;
  border: 1px solid #00c1aa;
  width: 283px;
  height: 42px;
}

.Buttons-Container {
  display: flex;
  justify-content: space-around;
  margin-left: 170px;
  margin-right: 170px;
}

.Agregar-Boton {
  margin: 0%;
  width: 121px;
  height: 40px;
  background: #ff5252;
  border-color: #ff5252;
}

.Cancel-Button {
  margin: 0%;
  width: 121px;
  height: 40px;
  background: #c4c4c4;
  border-color: solid #c4c4c4;
}
</style>