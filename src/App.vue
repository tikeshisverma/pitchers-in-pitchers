<template>
  <div id="app">
    <video ref="videoElement" id="video" controls hright="360" width="640" hidden></video>
    <div class="button-container">
      <button id="button" @click="handleStart" :disabled="desabled">START</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      videoElement: "",
      desabled: false,
    };
  },
  created() {
    this.selectMediaStream();
  },
  methods: {
    async selectMediaStream() {
      try {
        console.log("ababab");
        const mediaStream = await navigator.mediaDevices.getDisplayMedia();

        this.$refs["videoElement"].srcObject = mediaStream;
        this.$refs["videoElement"].onloadedmetadata = () => {
          this.$refs["videoElement"].play();
        };
      } catch (error) {
        console.log("whoops,error heror:", error);
      }
    },
    async handleStart() {
      this.desabled = true;
      await this.$refs["videoElement"].requestPictureInPicture();
      this.disabled = false;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Kufam&display=swap");
#app {
  font-family: "Kufam", cursive;
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgb(37, 37, 37);
  height: 100vh;
}
button {
  font-family: "Kufam", cursive;
  cursor: pointer;
  outline: none;
  width: 120px;
  height: 75px;
  font-size: 25px;
  color: white;
  text-shadow: 0 2px 5px black;
  background: linear-gradient(to top, #696969, #575757);
  border: 2px solid black;
  border-radius: 7px;
  box-shadow: inset 0 20px 4px -19px rgba(255, 255, 255, 0.7),
    0 12px 12px 0 rgba(0, 0, 0, 0.3);
}
button:hover {
  background: linear-gradient(to bottom, #696969, #575757);
}

button:active {
  transform: translate(3px);
  box-shadow: 0 6px 6px 0 rgba(0, 0, 0, 0.3);
}

.button-container {
  border: 2px solid black;
  padding: 10px;
  border-radius: 7px;
  box-shadow: inset 0 20px 4px -19px rgba(255, 255, 255, 0.7);
}
</style>
