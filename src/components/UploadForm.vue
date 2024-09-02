<template>
  <div class="p-6 max-w-sm mx-auto bg-white rounded-xl shadow-md space-y-4">
    <h2 class="text-xl font-bold text-gray-900">Upload File</h2>
    <form @submit.prevent="uploadFile">
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="category">Category</label>
        <select id="category" v-model="category" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
          <option value="investigations">Investigaciones</option>
          <option value="interviews">Entrevistas</option>
          <option value="curriculums">Curriculumns</option>
          <option value="others">Others</option>
        </select>
      </div>
      <div class="mb-4">
        <input type="file" @change="handleFileUpload" class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100"/>
      </div>
      <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Upload
      </button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      category: 'investigaciones',
    };
  },
  methods: {
    async uploadFile() {
      const fileInput = this.$refs.file;
      const formData = new FormData();
      formData.append('file', fileInput.files[0]);
      formData.append('category', this.category);

      try {
        const response = await axios.post('http://localhost:3000/upload', formData);
        console.log('File uploaded:', response.data);
      } catch (error) {
        console.error('Error uploading file:', error);
      }
    },
  },
};
</script>
