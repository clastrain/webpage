<template>
    <div class="token-card-container">
      <div v-if="loading" class="loading">
        Loading tokens...
      </div>
      <div v-else-if="error" class="error">
        {{ error }}
      </div>
      <div v-else class="token-cards">
        <div v-for="token in tokens" :key="token.mint" class="token-card">
          <div class="token-logo">
            <img 
              v-if="getTokenInfo(token.mint)?.data?.tokenInfo?.logoURI" 
              :src="getTokenInfo(token.mint).data.tokenInfo.logoURI" 
              :alt="getTokenInfo(token.mint)?.data?.tokenInfo?.name"
              class="logo"
              @error="handleImageError"
            >
            <div v-else class="logo-placeholder">
              {{ getTokenInfo(token.mint)?.data?.tokenInfo?.symbol?.[0] || 'T' }}
            </div>
          </div>
          <div class="token-details">
            <div class="token-header">
              <h3 class="token-name">
                {{ getTokenInfo(token.mint)?.data?.tokenInfo?.name || 'Unnamed Token' }}
              </h3>
              <span class="token-symbol">
                {{ getTokenInfo(token.mint)?.data?.tokenInfo?.symbol || '-' }}
              </span>
            </div>
            
            <div class="token-amount">
              Amount: {{ formatAmount(token.amount) }}
            </div>
  
            <div class="token-price-info">
              <p class="token-price">
                ${{ formatPrice(getTokenInfo(token.mint)?.data?.price) }}
              </p>
              <div class="price-details">
                <p class="buy-price">
                  Buy: ${{ formatPrice(getTokenInfo(token.mint)?.data?.priceData?.data?.[token.mint]?.extraInfo?.quotedPrice?.buyPrice) }}
                </p>
                <p class="sell-price">
                  Sell: ${{ formatPrice(getTokenInfo(token.mint)?.data?.priceData?.data?.[token.mint]?.extraInfo?.quotedPrice?.sellPrice) }}
                </p>
              </div>
            </div>
  
            <div class="token-meta">
              <p class="token-address" :title="token.mint">
                CA: {{ formatAddress(token.mint) }}
              </p>
              <p class="token-created">
                Created: {{ formatDate(getTokenInfo(token.mint)?.data?.tokenInfo?.created_at) }}
              </p>
              <div class="token-tags">
                <span v-for="tag in getTokenInfo(token.mint)?.data?.tokenInfo?.tags" 
                      :key="tag" 
                      class="tag">
                  {{ tag }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue'
  import axios from 'axios'
  
  export default {
    name: 'TokenInfoCard',
    setup() {
      const tokens = ref([])
      const tokenInfoMap = ref([])
      const loading = ref(true)
      const error = ref(null)
  
      const fetchTokenInfo = async (mint) => {
        try {
          const response = await axios.get(`https://neonwebhook.neonai.workers.dev/token-info/${mint}`)
          tokenInfoMap.value[mint] = response.data.data[0]
          console.log(tokenInfoMap.value[mint])
        } catch (err) {
          console.error(`Failed to fetch token info (${mint}):`, err)
        }
      }
  
      const fetchAllTokens = async () => {
        try {
          loading.value = true
          const response = await axios.get('https://neonwebhook.neonai.workers.dev/mytoken')
          if (response.data.success) {
            tokens.value = response.data.tokens
            
            const promises = tokens.value.map(token => 
              fetchTokenInfo(token.mint)
            )
            
            await Promise.all(promises)
          }
        } catch (err) {
          error.value = 'Failed to fetch token data: ' + err.message
        } finally {
          loading.value = false
        }
      }
  
      const getTokenInfo = (mint) => {
        return tokenInfoMap.value[mint]
      }
  
      const formatAddress = (address) => {
        if (!address) return '-'
        return `${address.slice(0, 6)}...${address.slice(-4)}`
      }
  
      const formatAmount = (amount) => {
        if (!amount) return '0'
        return new Intl.NumberFormat('en-US', {
          minimumFractionDigits: 2,
          maximumFractionDigits: 6
        }).format(amount)
      }
  
      const formatPrice = (price) => {
        if (!price) return '0.00'
        return new Intl.NumberFormat('en-US', {
          minimumFractionDigits: 6,
          maximumFractionDigits: 9
        }).format(parseFloat(price))
      }
  
      const formatDate = (dateString) => {
        if (!dateString) return '-'
        return new Date(dateString).toLocaleDateString('en-US')
      }
  
      const handleImageError = (event) => {
        event.target.style.display = 'none'
        event.target.nextElementSibling.style.display = 'flex'
      }
  
      onMounted(() => {
        fetchAllTokens()
      })
  
      return {
        tokens,
        loading,
        error,
        getTokenInfo,
        formatAddress,
        formatAmount,
        formatPrice,
        formatDate,
        handleImageError
      }
    }
  }
  </script>
  
  <style scoped>
  .token-card-container {
    padding: 20px;
  }
  
  .loading, .error {
    text-align: center;
    padding: 20px;
  }
  
  .error {
    color: #ff4444;
  }
  
  .token-cards {
    display: grid;
    gap: 20px;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  }
  
  .token-card {
    display: flex;
    align-items: flex-start;
    padding: 20px;
    border: 1px solid #eee;
    border-radius: 12px;
    background: white;
    box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  }
  
  .token-logo {
    margin-right: 20px;
  }
  
  .logo, .logo-placeholder {
    width: 60px;
    height: 60px;
    border-radius: 30px;
    object-fit: cover;
  }
  
  .logo-placeholder {
    background: #f0f0f0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    color: #666;
  }
  
  .token-details {
    flex: 1;
  }
  
  .token-header {
    display: flex;
    align-items: center;
    margin-bottom: 12px;
  }
  
  .token-name {
    margin: 0;
    font-size: 1.3em;
    color: #333;
  }
  
  .token-symbol {
    margin-left: 8px;
    padding: 2px 8px;
    background: #f0f0f0;
    border-radius: 4px;
    font-size: 0.9em;
    color: #666;
  }
  
  .token-amount {
    font-size: 1.1em;
    color: #333;
    margin-bottom: 10px;
  }
  
  .token-price-info {
    margin-bottom: 15px;
  }
  
  .token-price {
    font-size: 1.4em;
    font-weight: bold;
    color: #2c3e50;
    margin: 0 0 8px 0;
  }
  
  .price-details {
    display: flex;
    gap: 15px;
    font-size: 0.9em;
    color: #666;
  }
  
  .token-meta {
    font-size: 0.9em;
    color: #666;
  }
  
  .token-address {
    font-family: monospace;
    background: #f5f5f5;
    padding: 4px 8px;
    border-radius: 4px;
    margin: 5px 0;
  }
  
  .token-created {
    margin: 5px 0;
  }
  
  .token-tags {
    display: flex;
    gap: 8px;
    margin-top: 8px;
  }
  
  .tag {
    padding: 2px 8px;
    background: #e1e1e1;
    border-radius: 12px;
    font-size: 0.8em;
    color: #555;
  }
  
  .buy-price {
    color: #16a34a;
  }
  
  .sell-price {
    color: #dc2626;
  }
  </style>