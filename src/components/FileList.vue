<template>
  <div class="p-6 max-w-lg mx-auto bg-white rounded-xl shadow-md space-y-4">
    <h2 class="text-xl font-bold text-gray-900">Files in {{ category }}</h2>
    
    <div v-if="files.length" class="space-y-2">
      <div 
        v-for="file in files" 
        :key="file.key" 
        class="flex items-center justify-between p-2 bg-gray-100 rounded-lg"
      >
        <span class="text-gray-800">{{ file.name }}</span>
        <button 
          @click="downloadFile(file.key)" 
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-1 px-3 rounded"
        >
          Download
        </button>
      </div>
    </div>

    <div v-else class="text-gray-500">
      No files found in this category.
    </div>
  </div>
</template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: ['category'],
    data() {
      return {
        files: [],
      };
    },
    async created() {
      try {
        const response = await axios.get(`http://localhost:3000/files/${this.category}`);
        this.files = response.data;
      } catch (error) {
        console.error('Error fetching files:', error);
      }
    },
  };
  </script>
  