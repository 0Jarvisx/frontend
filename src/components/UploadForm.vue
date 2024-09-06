<template>
  <div class="relative p-6 max-w-sm mx-auto bg-white rounded-xl shadow-md space-y-4">
    <h2 class="text-xl font-bold text-gray-900">Subir archivo</h2>
    <form @submit.prevent="uploadFile">
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="category">Category</label>
        <select id="category" v-model="category" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
          <option value="investigaciones">Investigaciones</option>
          <option value="entrevistas">Entrevistas</option>
          <option value="curriculumns">Curriculumns</option>
          <option value="otros">Otros</option>
        </select>
      </div>
      <div class="mb-4">
        <input type="file" ref="file" @change="handleFileUpload" class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100"/>
      </div>
      <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" :disabled="isUploading">
        Subir
        <span v-if="isUploading" class="ml-2 spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
      </button>
    </form>

    <div v-if="isUploading" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50">
      <div class="bg-white p-6 rounded-lg shadow-lg flex items-center justify-center">
        <div class="w-12 h-12 border-4 border-blue-500 border-t-transparent border-solid rounded-full animate-spin"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      category: 'investigaciones',
      isUploading: false, 
    };
  },
  methods: {
    async uploadFile() {
      const fileInput = this.$refs.file;
      const formData = new FormData();
      
      formData.append('file', fileInput.files[0]);
      formData.append('category', this.category);

      this.isUploading = true; 

      try {
        const response = await axios.post('http://54.89.158.166:3000/upload?category=' + this.category, formData, {withCredentials: false});
        console.log('File uploaded:', response.data);
        if (response.data.message) this.$emit('file-uploaded', this.category);
        
      } catch (error) {
        console.error('Error uploading file:', error);
      } finally {
        this.isUploading = false;
      }
    },
  },
};
</script>