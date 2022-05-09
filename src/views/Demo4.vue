<template>
  <div>
    <div id="drag-items">
      <img
        src="https://picsum.photos/600/300/?image=25"
        @dragstart="dragstart"
        width="50"
        height="50"
        draggable="true"
      />
      <!-- <img src="https://picsum.photos/600/300/?image=25" @dragstart="dragstart" width="50" height="50" draggable="true" /> -->
    </div>
    <div @dragover.prevent @drop="hdrop" style="width: 100vw; height: 100vh">
        <v-stage ref="stage" :config="configKonva">
      <v-layer >
        <!-- <v-circle :config="configCircle"></v-circle> -->
        <v-image
          v-for="(image, index) in images"
          :key="index"
          :config="{
            x:image.x,
            y:image.y,
            image: image.image,
            draggable:true,
          }"
        />
      </v-layer>
        </v-stage>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      configKonva: {
        width: 1500,
        height: 800,
      },
      images: [],
      itemURL: "",
    };
  },
  methods: {
    dragstart(e) {
      console.log('eeeeeeeeee', e);
      this.itemURL = e.target.src;
    },
    // dragover(e) {
    //   e.preventDefault();
    // }
    hdrop(e) {
      console.log('ggggggggggg', e);
      e.preventDefault();

      const image = new window.Image(50,50);
      console.log('IMAGE', image);
      image.style.top=e.offsetY+'px';
      image.style.left=e.offsetX+'px';
      // image.position({ x: e.offsetX, y: e.offsetY });
      // image.draggable(true);
      image.src = this.itemURL;
      var obj = {};
      obj.image = image;
      obj.x = e.offsetX;
      obj.y = e.offsetY;
      this.images.push(obj);

      // Konva.Image.fromURL(itemURL, function (image) {
      //   layer.add(image);
      // });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>