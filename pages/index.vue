<template>
  <div class="mx-auto">
    <input type="file" name="" @change="selectImage($event)" id="">
    <div class="imageEditorApp mx-auto" :class="shouldDisplay == true ? '' : 'hidden'">
      <tui-image-editor ref="editor" :include-ui="useDefaultUI" :options="options"></tui-image-editor>
    </div>
  </div>
</template>
<script>
const icona = require("tui-image-editor/dist/svg/icon-a.svg");
const iconb = require("tui-image-editor/dist/svg/icon-b.svg");
const iconc = require("tui-image-editor/dist/svg/icon-c.svg");
const icond = require("tui-image-editor/dist/svg/icon-d.svg");
const blackTheme = {
 "menu.normalIcon.path": icond,
 "menu.activeIcon.path": iconb,
 "menu.disabledIcon.path": icona,
 "menu.hoverIcon.path": iconc
};
export default {
  data: function(){
  
    return{
      shouldDisplay: true,
      useDefaultUI: false,
      options: { // for tui-image-editor component's "options" prop
          cssMaxWidth: 800,
          cssMaxHeight: 700,
          includeUI: {
            loadImage: {
              path: '', 
              name: ''
            },
            initMenu: "text",
            theme: blackTheme,           
            menuBarPosition: 'bottom',
            menu: ['crop', 'flip', 'rotate', 'text'], //, 'filter',
          },          
      }
    }
  },
  methods:{
    selectImage: function(event){
      console.log("New image added.");
      this.shouldDisplay = true;
      const file = event.target.files[0];
      var a = this;
        this.$refs.editor.invoke("startDrawingMode", "CROPPER");
      this.$refs.editor.invoke('loadImageFromFile', file).then(() => {
        console.log("image loaded.");
        this.$refs.editor.invoke('addText', 'init text');

      });
    },
 
  },

  mounted(){

  }
}
</script>

<style>
.imageEditorApp {
 width: 95vw;
 height: calc(100vh - 150px);
}
</style>
