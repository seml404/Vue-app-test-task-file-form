<template>
  <div>
    <div class="upload-section">
      <form class="upload-form" action="#" @submit.prevent="handleSend">
        <input
          type="file"
          style="display: none"
          id="upload-input"
          multiple
          @change="handleSelect"
        />
        <div class="btn-container">
          <button type="button" class="btn" @click="handleUpload">
            Choose images
          </button>
        </div>
        <div class="preview-section-container">
          <div class="preview-section" v-if="fileList.length > 0">
            <image-preview
              v-for="(item, idx) in fileList"
              :imageItem="item"
              :key="item"
              :idx="idx + 1"
              @handleRemove="handleRemove"
              @handleDragStart="handleDragStart"
              @handleDrop="handleDrop"
            />
          </div>
          <p v-else>No images are chosen!</p>
        </div>
        <div class="btn-container">
          <button class="btn" type="submit" :disabled="btnDisabled">
            Send images
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import ImagePreview from "./ImagePreview.vue";
export default {
  components: { ImagePreview },
  data() {
    return {
      fileList: [],
      replacingImg: "",
      replacedImg: "",
    };
  },
  methods: {
    handleSelect(e) {
      this.fileList = [];
      this.fileList = [...e.target.files];
      console.log(this.fileList);
    },
    handleUpload() {
      document.getElementById("upload-input").click();
    },
    handleRemove(value) {
      console.log("deleted", value);
      this.fileList = this.fileList.filter((item) => item.name !== value);
    },
    handleDragStart(value) {
      this.replacingImg = {
        file: this.fileList.find((item) => item.name === value),
        index: this.fileList.findIndex((item) => item.name === value),
      };
    },
    handleDrop(value) {
      this.replacedImg = {
        file: this.fileList.find((item) => item.name === value),
        index: this.fileList.findIndex((item) => item.name === value),
      };
      this.fileList[this.replacedImg.index] = this.replacingImg.file;
      this.fileList[this.replacingImg.index] = this.replacedImg.file;
    },
    async handleSend() {
      let formD = new FormData();
      this.fileList.forEach((item) => {
        formD.append(`${item.name}`, item);
      });
      try {
        let requestResult = await fetch("url", {
          method: "POST",
          body: formD,
        });
        if (requestResult.ok) {
          let resParsed = await requestResult.json();
          console.log(resParsed);
        }
      } catch (error) {
        throw new Error(error);
      }
    },
  },
  computed: {
    btnDisabled() {
      return this.fileList.length === 0;
    },
  },
};
</script>

<style scoped>
.upload-section {
  display: flex;
  flex-direction: column;
}

.preview-section {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  padding: 15px;
  border: 1px solid grey;
  box-shadow: 2px 2px 2px 2px grey;
  border-radius: 10px;
}

.btn-container {
  padding: 10px 0;
}
</style>
