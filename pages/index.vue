<template>
  <div class="mx-auto lg:container dark:bg-gray-800 h-screen w-screen">

    <!-- First screen -->
    <div class="w-screen py-20" :class="!shouldDisplay ? '' : 'hidden'">
      <div class="border-dashed border-2 text-green-300 dark:text-white text-center border-green-400 dark:border-white px-6 py-10 my-4 w-max rounded-lg mx-auto">
        <span @click="$refs.browseFile.chooseFile()" class="text-sm text-center mx-auto">
          <svg xmlns="http://www.w3.org/2000/svg" class="mx-auto" fill="none" width="75" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
          </svg>
        </span>
        <span class="text-sm">Drag & drop or Browse</span>
      </div>

      <h3 class="text-4xl text-center text-gray-800 dark:text-white mt-8">You’re in!</h3>
      <p class="text-gray-800 dark:text-white text-center my-4">Adding your greeting is quick and easy.Take a photo,type your message and done!.</p>

      <div @click="$refs.browseFile.chooseFile()" class="flex flex-nowrap content-center cursor-pointer space-x-2 rounded-lg text-white bg-green-400 w-max px-4 py-3 mx-auto">
        <span class="mt-1">
          <svg xmlns="http://www.w3.org/2000/svg" class="mx-auto" fill="none" width="20" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
          </svg>          
        </span>
        <span>Browse Image</span>
        </div>
    </div>

    <!-- Second screen -->
    <div
      class=""
      :class="shouldDisplay ? '' : 'hidden'"
    >
      <div class="flex flex-nowrap space-x-4 place-content-between px-4 py-4">
        <div class="bg-red-600 text-white text-sm rounded-lg p-2">Close</div>
        <div class="bg-yellow-500 text-white text-sm rounded-lg p-2" @click="$refs.browseFile.chooseFile()">change</div>
        <div class="bg-green-400  text-white text-sm rounded-lg p-2">save</div>
      </div>
      <div class="imageEditorApp mx-auto">
        <client-only>
          <croppa class="mx-auto" :width="width" :height="height" :accept="'image/*'" :show-remove-button="false" v-model="myCroppa" @file-choose="selectImage" ref="browseFile"></croppa>
        </client-only>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data: function() {
    return {
      shouldDisplay: false,
      height: 0,
      width: 0,
      myCroppa:{}
    };
  },
  methods: {
    selectImage: function() {
      console.log("New image added.");
      this.shouldDisplay = true;
 
    }
  },

  mounted() {
    this.height = Math.round(window.innerHeight * 0.6) 
    this.width = Math.round(window.innerWidth * 0.8)
  }
};
</script>

<style>

</style>
