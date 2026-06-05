<template>
  <div>
    <header>
      <h1>Cooking Masterclass</h1>
      <div class="cart-icon">Cart: {{ totalItems }}</div>
    </header>
    
    <div class="container">
      <div class="courses">
        <div class="course-card" v-for="course in courses" :key="course.id">
          <img :src="course.image" :alt="course.name">
          <div class="course-info">
            <h3 class="course-name">{{ course.name }}</h3>
            <div class="course-price">R{{ course.price }}</div>
            <button class="add-btn" @click="addToCart(course)">Add to Cart</button>
          </:
