<template>
  <div id="app">
    <file-pond
      name="test"
      ref="pond"
      label-idle="Drop files here or <span class='filepond--label-action'>Browse</span>"
      allow-multiple="true"
      accepted-file-types="image/jpeg, image/png"
      v-bind:files="myFiles"
      v-on:init="handleFilePondInit"
      v-on:addfile="filesChange"
    />
  </div>
</template>

<script>
// Import Vue FilePond
import vueFilePond from "vue-filepond";

// Import FilePond styles
import "filepond/dist/filepond.min.css";

// Import FilePond plugins
// Please note that you need to install these plugins separately

// Import image preview plugin styles
import "filepond-plugin-image-preview/dist/filepond-plugin-image-preview.min.css";

// Import image preview and file type validation plugins
import FilePondPluginFileValidateType from "filepond-plugin-file-validate-type";
import FilePondPluginImagePreview from "filepond-plugin-image-preview";

// Create component
const FilePond = vueFilePond(
  FilePondPluginFileValidateType,
  FilePondPluginImagePreview
);
export default {
  name: "FilePondDemo",
  data: function() {
    return { myFiles: [] };
  },

  methods: {
    handleFilePondInit: function() {
      console.log("FilePond has initialized");

      // example of instance method call on pond reference
      this.$refs.pond.getFiles();
    },

    filesChange: function() {
      console.log("in filechange");

      var files = this.$refs.pond.getFiles();

      for (var i = 0; i < files.length; i++) {
        console.log(files[i].filename);
      }
    }
  },

  components: {
    FilePond
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
