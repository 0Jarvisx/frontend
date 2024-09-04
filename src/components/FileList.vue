<template>
  <div class="p-6 max-w-lg mx-auto bg-white rounded-xl shadow-md space-y-6">  
    <h2 class="text-xl font-bold text-gray-900">Files in {{ category }}</h2>
    
    <div v-if="files.length > 0" class="space-y-6">
      <div 
        v-for="file in files" 
        :key="file.key" 
        class="relative p-2 bg-gray-100 rounded-lg"
      >
       
        <iframe 
          v-if="file.key.endsWith('.pdf')"
          :src="file.url" 
          class="w-full h-96 border rounded-lg resize-none"
          frameborder="0"
          scrolling="auto"
        ></iframe>

        <img 
          v-else-if="file.key.endsWith('.jpg') || file.key.endsWith('.png')"
          :src="file.url"
          class="w-full h-auto border rounded-lg"
          alt="Image"
        />

        <video 
          v-else-if="file.key.endsWith('.mp4') || file.key.endsWith('.mov')"
          :src="file.url"
          class="w-full h-64 border rounded-lg"
          controls
        ></video>

        <div 
          v-else
          class="flex items-center justify-center w-full h-64 border rounded-lg bg-gray-200"
        >
          <span class="text-4xl text-gray-500">✗</span>
        </div>

        <div class="absolute bottom-2 left-2 right-2 text-gray-800 bg-white bg-opacity-75 text-center py-1 rounded">
          {{ file.key.split('/').pop() }}
        </div>
      </div>
    </div>

    <div v-else class="text-gray-500">
     No se encontraron elementos
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
    this.refreshFiles();
  },
  methods: {
    async refreshFiles() {
      try {
        const response = await axios.get(`http://localhost:3000/files/${this.category}`);
        this.files = response.data;
        console.log('----------this.files', this.files);
      } catch (error) {
        console.error('Error fetching files:', error);
      }
    }
  }
};
</script>

<style scoped>
iframe {
  width: 100%;
  border: 1px solid #ddd;
  border-radius: 8px;
}

img {
  max-width: 100%;
  height: auto;
}

video {
  width: 100%;
  height: auto;
}

.icon-container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f3f3f3;
}
</style>
