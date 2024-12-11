<template>
  <div class="publications-container">
    <div v-if="loading" class="loading">
      Loading...
    </div>
    <div v-else-if="error" class="error">
      {{ error }}
    </div>
    <div v-else class="publications-list">
      <div v-for="publication in publications" :key="publication.id" class="publication-card">
        <div class="publication-header">
          <span class="date">{{ formatDate(publication.created_at) }}</span>
          <span class="status" :class="{ 'status-active': publication.status }">
            {{ publication.status ? 'Hold' : 'Dump' }}
          </span>
        </div>
        <div class="publication-content">
          <p class="tweet">{{ publication.tweet }}</p>
          <p class="ca">CA: {{ publication.ca }}</p>
          <p v-if="publication.price" class="price">Price: {{ publication.price }}</p>
          <p v-if="publication.tx" class="tx">TX: {{ publication.tx }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import axios from 'axios'

export default {
  name: 'PublicationsComponent',
  setup() {
    const publications = ref([])
    const loading = ref(true)
    const error = ref(null)

    const fetchPublications = async () => {
      try {
        loading.value = true
        const response = await axios.get('https://neonwebhook.neonai.workers.dev/mypublications')
        if (response.data.success) {
          publications.value = response.data.data
        } else {
          error.value = 'Veri alınamadı'
        }
      } catch (err) {
        error.value = 'Bir hata oluştu: ' + err.message
      } finally {
        loading.value = false
      }
    }

    const formatDate = (dateString) => {
      return new Date(dateString).toLocaleString('tr-TR')
    }

    onMounted(() => {
      fetchPublications()
    })

    return {
      publications,
      loading,
      error,
      formatDate
    }
  }
}
</script>

<style scoped>


.loading, .error {
  text-align: center;
  padding: 20px;
}

.error {
  color: red;
}

.publications-list {
  display: grid;
  gap: 10px;
}

.publication-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  background: white;
}

.publication-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.date {
  color: #666;
  font-size: 0.9em;
}

.status {
  padding: 4px 8px;
  border-radius: 4px;
  background: #ff4444;
  color: white;
  font-size: 0.8em;
}

.status-active {
  background: #44bb44;
}

.publication-content {
  font-size: 0.95em;
}

.tweet {
  margin-bottom: 10px;
}

.ca, .price, .tx {
  color: #666;
  font-size: 0.9em;
  margin: 5px 0;
  word-break: break-all;
}
</style>