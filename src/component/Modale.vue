<script setup>
const props = defineProps({
    color: Object
});

const emit = defineEmits(['close']);
</script>

<template>
    <div v-if="color" class="modal-overlay" @click.self="emit('close')">
        <div class="modal-card">
            <button class="back-btn" @click="emit('close')">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M19 12H5M12 19l-7-7 7-7" />
                </svg>
                Retour
            </button>

            <div class="modal-content">
                <div class="color-preview" :style="{ backgroundColor: color.hex }"></div>

                <div class="text-info">
                    <span class="category">Détails de la nuance</span>
                    <h2>{{ color.name }}</h2>
                    <div class="hex-badge">{{ color.hex }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.4);
    backdrop-filter: blur(8px);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
}

.modal-card {
    background: white;
    width: 90%;
    max-width: 450px;
    border-radius: 24px;
    padding: 32px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.2);
    position: relative;
}

.back-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    background: none;
    border: none;
    color: #666;
    font-size: 0.9rem;
    cursor: pointer;
    padding: 0;
    margin-bottom: 24px;
    transition: color 0.2s;
}

.back-btn:hover {
    color: #000;
}

.modal-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.color-preview {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    margin-bottom: 20px;
    box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.1);
}

.category {
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 2px;
    color: #999;
}

h2 {
    font-size: 1.8rem;
    margin: 10px 0;
    font-weight: 700;
}

.hex-badge {
    display: inline-block;
    padding: 8px 16px;
    background: #f5f5f7;
    border-radius: 100px;
    font-family: 'SF Mono', monospace;
    font-size: 0.9rem;
    color: #333;
}
</style>