<template>
  <div
    class="img-container"
    draggable="true"
    @dragstart="handleDragStart"
    @dragend="handleDragEnd"
    @dragover.prevent=""
    @drop.prevent="handleDrop"
  >
    <p class="img-title">№ {{ idx }}</p>
    <img class="img-item" :src="path" alt="image" draggable="false" />
    <button class="btn btn-remove" @click="handleRemove">X</button>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    imageItem: {
      type: Object,
      required: true,
    },
    idx: {
      type: Number,
      required: true,
    },
  },
  emits: ["handleRemove", "handleDragStart", "handleDrop"],
  methods: {
    handleRemove() {
      this.$emit("handleRemove", this.imageItem.name);
    },
    handleDragStart(e) {
      e.target.style.backgroundColor = "#d5e3f0";
      this.$emit("handleDragStart", this.imageItem.name);
    },
    handleDragEnd(e) {
      e.target.style.backgroundColor = "white";
    },
    handleDrop() {
      this.$emit("handleDrop", this.imageItem.name);
    },
  },

  computed: {
    path() {
      return URL.createObjectURL(this.imageItem);
    },
  },
};
</script>

<style scoped>
.btn-remove {
  color: red;
  background: none;
  border: none;
  cursor: pointer;
  font-weight: 700;
  font-size: 16px;
}

.img-container {
  cursor: grab;
  border-radius: 10px;
}

.img-item {
  width: 100px;
  height: 100px;
  display: flex;
  border-radius: 10px;
}

.img-title {
  font-size: 8pt;
}
</style>
