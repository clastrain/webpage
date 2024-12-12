<template>
    <div class="copy-container">
        <!-- Text alanı -->
        <div class="token-address"  @click="copyText">
            {{ formatCA(text) }}
        </div>

        <!-- Kopyalama durumu bildirimi -->
        <div class="copy-feedback" :class="{ 'show': isCopied }">
            Copied!
        </div>
    </div>
</template>

<script>
export default {
    name: 'CopyButton',
    props: {
        text: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            isCopied: false
        }
    },
    methods: {
        formatCA(address) {
            console.log(address)
            if (!address) return '-'
            return `${address.slice(0, 6)}...${address.slice(-4)}`
        },
        async copyText() {
            try {
                await navigator.clipboard.writeText(this.text);
                this.showCopiedFeedback();
            } catch (err) {
                console.error('Kopyalama başarısız:', err);
            }
        },
        showCopiedFeedback() {
            this.isCopied = true;
            setTimeout(() => {
                this.isCopied = false;
            }, 2000);
        }
    }
}
</script>

<style scoped>
.copy-container {
    position: relative;
    display: inline-block;
}

.text-content {
    cursor: pointer;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
    user-select: all;
}

.text-content:hover {
    background-color: #f5f5f5;
}

.copy-feedback {
    position: absolute;
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%);
    background-color: #333;
    color: white;
    padding: 5px 10px;
    border-radius: 4px;
    font-size: 12px;
    opacity: 0;
    transition: opacity 0.3s;
    pointer-events: none;
}

.copy-feedback.show {
    opacity: 1;
}
.token-address {
    font-family: monospace;
    background: #f5f5f5;
    padding: 4px 8px;
    border-radius: 4px;
    margin: 5px 0;
  }
</style>