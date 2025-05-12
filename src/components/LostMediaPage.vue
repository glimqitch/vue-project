<template>
  <div class="lost-media-container">
    <h2 class="page-title">Lost Media</h2>

    <!-- Media form section -->
    <form @submit.prevent="addMedia" class="media-form">
      <input v-model="newMedia" class="media-input" placeholder="Afegir Lost Media" />
      
      <!-- Dropdown to select if media is lost or found -->
      <select v-model="mediaStatus" class="media-select">
        <option value="lost">Lost</option>
        <option value="found">Found</option>
      </select>

      <button type="submit" class="add-button">Afegir</button>
    </form>

    <!-- Media List Section -->
    <ul v-if="lostMedia.length" class="media-list">
      <li v-for="(media, index) in lostMedia" :key="index" class="media-item">
        <div class="media-content">
          <span class="media-name">{{ media.name }}</span> 
          <strong class="media-status">{{ media.status }}</strong>
        </div>
        <button @click="deleteMedia(index)" class="delete-button">Delete</button>
      </li>
    </ul>

    <!-- Loading Message -->
    <p v-else class="loading-message">No Lost Media available...</p>
  </div>
</template>

<script>
export default {
  name: 'LostMediaPage',
  data() {
    return {
      newMedia: '',
      mediaStatus: 'lost', // Default status is 'lost'
      lostMedia: JSON.parse(localStorage.getItem('lostMedia')) || [] // Load from localStorage
    };
  },
  methods: {
    addMedia() {
      if (this.newMedia) {
        // Add media with its status
        this.lostMedia.push({ name: this.newMedia, status: this.mediaStatus });
        this.newMedia = '';  // Clear the input
        this.mediaStatus = 'lost';  // Reset status to 'lost' after adding

        // Save to localStorage
        localStorage.setItem('lostMedia', JSON.stringify(this.lostMedia));
      }
    },
    // Method to delete media
    deleteMedia(index) {
      this.lostMedia.splice(index, 1);
      // Save updated list to localStorage
      localStorage.setItem('lostMedia', JSON.stringify(this.lostMedia));
    }
  }
};
</script>

<style scoped>
/* Main container styling */
.lost-media-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Arial', sans-serif;
  background-color: #f7f9fc;
  border-radius: 8px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
}

/* Page title styling */
.page-title {
  text-align: center;
  font-size: 2rem;
  color: #333;
  margin-bottom: 20px;
}

/* Form styling */
.media-form {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.media-input,
.media-select {
  margin-right: 10px;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

.add-button {
  padding: 10px 20px;
  background-color: #007BFF;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.add-button:hover {
  background-color: #0056b3;
}

/* Media List styling */
.media-list {
  list-style-type: none;
  padding: 0;
}

.media-item {
  background-color: #fff;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
}

.media-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
}

.media-content {
  flex-grow: 1;
}

.media-name {
  font-size: 1.2rem;
  color: #333;
  font-weight: 600;
}

.media-status {
  font-size: 1rem;
  color: #666;
  margin-left: 10px;
}

/* Delete button styling */
.delete-button {
  padding: 8px 12px;
  background-color: #FF5733;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.delete-button:hover {
  background-color: #c0392b;
}

/* Loading message styling */
.loading-message {
  text-align: center;
  font-size: 1.2rem;
  color: #888;
}

/* Responsive Design */
@media (max-width: 768px) {
  .lost-media-container {
    padding: 15px;
  }

  .page-title {
    font-size: 1.8rem;
  }

  .media-form {
    flex-direction: column;
    align-items: center;
  }

  .media-input,
  .media-select {
    margin-bottom: 10px;
    width: 100%;
  }

  .add-button {
    width: 100%;
    margin-top: 10px;
  }

  .media-item {
    padding: 12px;
  }
}
</style>
