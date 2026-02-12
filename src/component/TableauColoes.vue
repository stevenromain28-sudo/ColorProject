<script setup>
import { ref } from "vue";
import Modale from "./Modale.vue";
const emit = defineEmits(["select"]);
const selectedId = ref();

const colors = [
    { id: 1, name: "Bleu Klein", hex: "#002FA7" },
    { id: 2, name: "Or Rose", hex: "#B76E79" },
    { id: 3, name: "Vert Émeraude", hex: "#50C878" },
    { id: 4, name: "Rouge Carmin", hex: "#960018" },
    { id: 5, name: "Violet Tyrien", hex: "#66023C" },
    { id: 6, name: "Bleu Turquoise", hex: "#40E0D0" },
    { id: 7, name: "Jaune Ambre", hex: "#FFBF00" },
    { id: 8, name: "Gris Anthracite", hex: "#2F4F4F" },
    { id: 9, name: "Rose Fuchsia", hex: "#FF00FF" },
    { id: 10, name: "Blanc Albâtre", hex: "#FEFEFA" }
];

function selectColor(id) {
    selectedId.value = colors.find(t => t.id === id);
}
</script>
<template>
    <div class="container">
        <header class="header">
            <h2>Palette Chromatique</h2>
            <p>Sélectionnez une nuance pour votre projet</p>
        </header>

        <div class="grid">
            <div v-for="color in colors" :key="color.id" class="card" :class="{ active: selectedId?.id === color.id }"
                @click="selectColor(color.id)">
                <div class="swatch-wrapper">
                    <div class="swatch" :style="{ backgroundColor: color.hex }">
                        <div class="overlay">
                            <span class="action-text">SÉLECTIONNER</span>
                        </div>
                    </div>
                </div>

                <div class="details">
                    <span class="name">{{ color.name }}</span>
                    <span class="hex">{{ color.hex }}</span>
                </div>
            </div>
        </div>
    </div>
   <Modale :color="selectedId" @close="selectedId = null" />
</template>

<style scoped>
.container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 60px 20px;
    font-family: -apple-system, BlinkMacSystemFont, "Inter", sans-serif;
    background-color: #ffffff;
}

.header {
    margin-bottom: 48px;
    text-align: center;
}

.header h2 {
    font-size: 1.5rem;
    font-weight: 600;
    letter-spacing: -0.02em;
    color: #111;
    margin-bottom: 8px;
}

.header p {
    color: #666;
    font-size: 0.95rem;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 32px;
}

.card {
    cursor: pointer;
    transition: transform 0.2s ease;
}

.swatch-wrapper {
    position: relative;
    width: 100%;
    aspect-ratio: 1;
    border-radius: 12px;
    overflow: hidden;
    background: #f5f5f7;
    /* Skeleton color */
    border: 1px solid rgba(0, 0, 0, 0.05);
}

.swatch {
    width: 100%;
    height: 100%;
    transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

.overlay {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(0, 0, 0, 0.2);
    opacity: 0;
    transition: opacity 0.3s ease;
}

.action-text {
    color: white;
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 0.1em;
}

/* Hover States */
.card:hover .swatch {
    transform: scale(1.05);
}

.card:hover .overlay {
    opacity: 1;
}

/* Active State */
.card.active .swatch-wrapper {
    ring: 2px solid #000;
    outline: 2px solid #000;
    outline-offset: 3px;
}

.details {
    margin-top: 14px;
    display: flex;
    flex-direction: column;
    gap: 2px;
}

.name {
    font-size: 0.85rem;
    font-weight: 500;
    color: #1d1d1f;
}

.hex {
    font-size: 0.75rem;
    font-family: "SF Mono", monospace;
    color: #86868b;
    text-transform: uppercase;
}
</style>