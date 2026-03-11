<script setup>
import { ref, onMounted } from 'vue'
import { store } from '../../store.js'
import Card from 'primevue/card'

const show = ref(false)
const flipped = ref(new Set())

function toggleFlip(key) {
    const next = new Set(flipped.value)
    if (next.has(key)) {
        next.delete(key)
    } else {
        next.add(key)
    }
    flipped.value = next
}

onMounted(() => {
    store.fetchData()
})
</script>

<template>
    <button @click="show = !show">Toggle</button>
<Transition>
    <div v-if="show" class="card-grid">
        <div class="flip-box" v-for="book in store.books" :key="book.order" @click="toggleFlip(book.order)">
            <div class="flip-box-inner" :class="{ flipped: flipped.has(book.order) }">
                <div class="flip-box-front">
                    <Card style="width: 16rem; height: 100%;">
                        <template #title>{{ book.title }}</template>
                        <template #subtitle>{{ book.series }} #{{ book.order }}</template>
                        <template #content>
                            <p class="m-0">{{ book.author }} &mdash; {{ book.year }}</p>
                        </template>
                    </Card>
                </div>
                <div class="flip-box-back">
                    <Card style="width: 16rem; height: 100%;">
                        <template #content>
                            <p>{{ book.description }}</p>
                        </template>
                    </Card>
                </div>
            </div>
        </div>
    </div>
    </Transition>
</template>

<style scoped>
.card-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}

.flip-box {
  width: 16rem;
  height: 200px;
  perspective: 1000px;
}

.flip-box-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.flip-box-inner.flipped {
  transform: rotateY(180deg);
}

.flip-box-front, .flip-box-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.flip-box-back {
  transform: rotateY(180deg);
}
</style>
