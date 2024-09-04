<template>
  <div id="app">
    <tittle-view></tittle-view>
    <upload-form @file-uploaded="refreshFileLists"></upload-form>
    <file-list ref="investigacionesList" category="investigaciones"></file-list>
    <file-list ref="entrevistasList" category="entrevistas"></file-list>
    <file-list ref="curriculumnsList" category="curriculumns"></file-list>
    <file-list ref="otrosList" category="otros"></file-list>
  </div>
</template>

<script>
import UploadForm from './components/UploadForm.vue';
import FileList from './components/FileList.vue';
import TittleView from './components/TittleView.vue';

export default {
  components: {
    UploadForm,
    FileList,
    TittleView
  },
  methods: {
    refreshFileLists(category) {
      // Actualiza el componente FileList correspondiente
      const fileListComponent = this.$refs[`${category}List`];
      if (fileListComponent) {
        fileListComponent.refreshFiles();
      }
    }
  }
};
</script>
