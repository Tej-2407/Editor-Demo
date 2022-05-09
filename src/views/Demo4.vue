<template>
  <div >
    <v-stage
      ref="stage"
      :config="config"
      @mousedown="handleStageMouseDown"
      @touchstart="handleStageMouseDown"
    >
      <v-layer ref="layer">
        <template v-for="item in list">
          <v-text
            :key="item.id"
            :ref="item.name"
            :config="item"
            @transformend="handleTransformEnd"
          />
        </template>

        <v-transformer
          ref="transformer"
          :config="{
            enabledAnchors: ['middle-left', 'middle-right'],
            boundBoxFunc: (oldBox, newBox) => {
              if (newBox.width < this.MIN_WIDTH) {
                return oldBox;
              }

              return newBox;
            },
          }"
        />
      </v-layer>
    </v-stage>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      MIN_WIDTH: 20,
      config: {
        width: window.innerWidth,
        height: window.innerHeight,
      },
      selectedShapeName: "",
      list: [
        {
          x: 50,
          y: 60,
          fontSize: 20,
          text: "Hello from the Konva framework. Try to resize me.",
          draggable: true,
          width: 200,
          scaleX: 1,
          name: "textResize1",
          height: "auto",
        },
      ],
    };
  },
  methods: {
    handleTransformEnd(e) {
      const item = this.list.find((i) => i.name === this.selectedShapeName);

      item.width = Math.max(
        e.target.width() * e.target.scaleX(),
        this.MIN_WIDTH
      );
      item.scaleX = 1;
      item.scaleY = 1;
    },
    handleStageMouseDown(e) {
      // clicked on stage - clear selection
      if (e.target === e.target.getStage()) {
        this.selectedShapeName = "";
        this.updateTransformer();
        return;
      }

      // clicked on transformer - do nothing
      const clickedOnTransformer =
        e.target.getParent().className === "Transformer";
      if (clickedOnTransformer) {
        return;
      }

      // find clicked rect by its name
      const name = e.target.name();
      const item = this.list.find((i) => i.name === name);
      if (item) {
        this.selectedShapeName = name;
      } else {
        this.selectedShapeName = "";
      }
      this.updateTransformer();
    },
    updateTransformer() {
      // here we need to manually attach or detach Transformer node
      const transformerNode = this.$refs.transformer.getNode();
      const stage = transformerNode.getStage();
      const { selectedShapeName } = this;

      const selectedNode = stage.findOne("." + selectedShapeName);
      // do nothing if selected node is already attached
      if (selectedNode === transformerNode.node()) {
        return;
      }

      if (selectedNode) {
        // attach to another node
        transformerNode.nodes([selectedNode]);
      } else {
        // remove transformer
        transformerNode.nodes([]);
      }
    },
  },
};
</script>
