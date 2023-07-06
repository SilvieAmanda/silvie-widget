<template>
  <div class="photo-widget">
    <h2 class="widget-title">{{ title }}</h2>
    <div class="photo-container">
      <img :src="photoUrl" :alt="title" />
    </div>
    <button class="load-button" @click="getRandomPhoto">Load New Photo</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      photoUrl: '',
    };
  },
  mounted() {
    this.getRandomPhoto();
  },
  methods: {
    async getRandomPhoto() {
      try {
        const apiKey = '38037020-2c48722c03be8437a05b588e6';
        const apiUrl = `https://pixabay.com/api/?key=${apiKey}&q=nature&image_type=photo&orientation=horizontal`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        const randomIndex = Math.floor(Math.random() * data.hits.length);
        const randomPhoto = data.hits[randomIndex];

        this.title = randomPhoto.tags;
        this.photoUrl = randomPhoto.webformatURL;
      } catch (error) {
        console.error('Error fetching random photo:', error);
      }
    },
  },
};
</script>

<style scoped>
.photo-widget {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #f9f9f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.widget-title {
  font-size: 24px;
  margin-bottom: 10px;
  text-align: center;
  color: #333;
}

.photo-container {
  width: 100%;
  max-width: 500px;
  margin-top: 10px;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.photo-container img {
  max-width: 100%;
  max-height: 100%;
  transition: transform 0.3s ease-in-out;
}

.photo-container img:hover {
  transform: scale(1.05);
}

.load-button {
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

.load-button:hover {
  background-color: #0056b3;
}
</style>
