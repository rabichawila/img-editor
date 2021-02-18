<template>
  <div class="mx-auto container my-20">
    <div class="border-dashed border-2 border-green-400 p-6 w-24 rounded-lg mx-auto">
      
      <span><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
</svg></span>
    </div>
    <input type="file" name="" @change="selectImage($event)" id="" />
    <div
      class="imageEditorApp mx-auto"
      :class="shouldDisplay == true ? '' : 'hidden'"
    >
      <tui-image-editor
        ref="editor"
        :include-ui="useDefaultUI"
        :options="options"
      ></tui-image-editor>
    </div>
  </div>
</template>
<script>
export default {
  data: function() {
    return {
      shouldDisplay: true,
      useDefaultUI: false,
      options: {
        // for tui-image-editor component's "options" prop
        cssMaxWidth: 800,
        cssMaxHeight: 700,
        includeUI: {
          loadImage: {
            path: "",
            name: ""
          },
          initMenu: "text",
          menuBarPosition: "bottom",
          menu: ["crop", "flip", "rotate", "text"] //, 'filter',
        }
      }
    };
  },
  methods: {
    selectImage: function(event) {
      console.log("New image added.");
      this.shouldDisplay = true;
      const file = event.target.files[0];
      var a = this;
      this.$refs.editor.invoke("startDrawingMode", "CROPPER");
      this.$refs.editor.invoke("loadImageFromFile", file).then(() => {
        console.log("image loaded.");
        this.$refs.editor.invoke("addText", "init text");
      });
    }
  },

  mounted() {}
};
</script>

<style>
.imageEditorApp {
  width: 90vw;
  background: #999;
  height: calc(100vh - 150px);
}
</style>
