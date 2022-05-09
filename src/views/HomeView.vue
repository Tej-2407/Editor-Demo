<template>
  <b-container class="bv-example-row" fluid>
    <b-row style="margin: 10px">
      <b-col>
        <b-jumbotron>
          <template #header>BootstrapVue</template>

          <template #lead> This is a simple Demo </template>

          <hr class="my-4" />

          <b-card
            title="Card Title"
            img-src="https://picsum.photos/600/300/?image=25"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 20rem"
            class="mb-2"
            @dragstart="dragstart"
            draggable="true"
          >
            <b-card-text @dragstart="dragstarttext" draggable="true">
              Some quick example text to build on the card title and make up the
              bulk of the card's content.
            </b-card-text>

            <b-button href="#" variant="primary">Go somewhere</b-button>
          </b-card>
          <b-button variant="primary" href="#" @click="download"
            >Do Something</b-button
          >
          <b-button variant="success" href="#">Do Something Else</b-button>
        </b-jumbotron>
      </b-col>
      <b-col style="border: 1px solid black" cols="8">
        <div @dragover.prevent @drop="hdrop">
          <v-stage ref="stage" :config="stageSize">
            <v-layer>
              <v-text :config="{ text: 'Some text on canvas', fontSize: 15 }" />
              <v-rect
                :config="{
                  x: 20,
                  y: 50,
                  width: 100,
                  height: 100,
                  fill: 'red',
                  shadowBlur: 10,
                }"
              />
              <v-circle
                :config="{
                  x: 200,
                  y: 100,
                  radius: 50,
                  fill: 'green',
                }"
              />
              <v-line
                :config="{
                  x: 300,
                  y: 50,
                  points: [0, 0, 100, 0, 100, 100],
                  tension: 0.5,
                  closed: true,
                  stroke: 'black',
                  fillLinearGradientStartPoint: { x: -50, y: -50 },
                  fillLinearGradientEndPoint: { x: 50, y: 50 },
                  fillLinearGradientColorStops: [0, 'red', 1, 'yellow'],
                }"
              />
              <v-image
                v-for="(image, index) in images"
                :key="index"
                :config="{
                  x: image.x,
                  y: image.y,
                  image: image.image,
                  draggable: true,
                }"
              />
              <v-text
                :config="{
                  text: text,
                  x: 500,
                  y: 400,
                }"
              />
            </v-layer>
            <v-layer ref="dragLayer"></v-layer>
          </v-stage>
        </div>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
const width = window.innerWidth;
const height = window.innerHeight;
export default {
  name: "HomeView",
  data() {
    return {
      stageSize: {
        width: width,
        height: height,
      },
      images: [],
      itemURL: "",
      text: "",
    };
  },
  methods: {
    dragstart(e) {
      this.itemURL = e.target.src;
    },
    dragstarttext(e) {
      // this.itemURL = e.target.toElement.innerText;
    },
    // dragover(e) {
    //   e.preventDefault();
    // }
    hdrop(e) {
       e.preventDefault();

      const image = new window.Image(50,50);
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
    download() {
      // var dataURL = this.images;
      // downloadURI(dataURL, "stage.png");
    },
    downloadURI(uri, name) {
      // var link = document.createElement('a');
      // link.download = name;
      // link.href = uri;
      // document.body.appendChild(link);
      // link.click();
      // document.body.removeChild(link);
      // delete link;
    },
  },
};
</script>
