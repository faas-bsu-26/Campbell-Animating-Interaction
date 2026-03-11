<script setup>
import { store } from '../../store.js'
import Card from 'primevue/card'
</script>

<template>
    
    <h1 class="overview">{{ store.overview }}</h1>
    
    <div class="card-grid">
        
      <div class="flip-box" v-for="book in store.books" :key="book.order">
        <div class="flip-box-inner">
          <div class="flip-box-front">
            <h2>{{ book.title }} {{ book.order }}</h2>
          </div>
          <div class="flip-box-back">
            <h2>{{ book.author }}</h2>
          </div>
        </div>
      </div>
    </div>


</template>
<style scoped>
.card-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}

.flip-box {
  background-color: transparent;
  width: 300px;
  height: 200px;
  border: 1px solid #f1f1f1;
  
}

/* This container is needed to position the front and back side */
.flip-box-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
}

/* Do an horizontal flip when you move the mouse over the flip box container */


/* Position the front and back side */
.flip-box-front, .flip-box-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

/* Style the front side */
.flip-box-front {
  background-color: #bbb;
  color: black;
}

/* Style the back side */
.flip-box-back {
  background-color: dodgerblue;
  color: white;
  transform: rotateY(180deg);
}
</style>