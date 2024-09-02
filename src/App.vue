<template>
  <div id="app">
    <upload-form></upload-form>
    <file-list category="investigaciones"></file-list>
    <file-list category="entrevistas"></file-list>
    <file-list category="curriculums"></file-list>
    <file-list category="otros"></file-list>
  </div>
</template>

<script>
import UploadForm from './components/UploadForm.vue';
import FileList from './components/FileList.vue';

export default {
  components: {
    UploadForm,
    FileList,
  },
};
</script>