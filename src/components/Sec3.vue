<template>
    <div class="spec3-container">
      <div style="display: flex; align-items: center; justify-content: center; margin-top: 10px">
        <h2 style="color:#043953;font-weight: 500">SECTION III [25 points]</h2>
      </div>
      
      <!-- Carousel Section -->
      <div class="carousel-wrapper">
        <!-- Left Arrow (outside of slider) -->
        <button class="arrow left-arrow" @click="prevSlide">
          <svg width="12" height="25" viewBox="0 0 12 25" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M11 1.88788L1.66669 12.5867L11 23.2855" fill="#043953"/>
            <path d="M11 1.88788L1.66669 12.5867L11 23.2855" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
        
        <div class="slider-container">
          <div class="slider" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
            <div
              class="slider-item"
              v-for="(slide, index) in slides"
              :key="index"
            >
            <div class="slide-content">
              <h3 class="slide-header" style="color: #043953">{{ slide.header }}</h3>
              <p class="slide-body">{{ slide.content }}</p>
            </div>
            </div>
          </div>
        </div>
        
        <button class="arrow right-arrow" @click="nextSlide">
          <svg width="12" height="25" viewBox="0 0 12 25" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M1 1.88792L10.3333 12.5867L1 23.2856" fill="#043953"/>
            <path d="M1 1.88792L10.3333 12.5867L1 23.2856" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
      </div>
      <div class="dots">
        <span
          v-for="(slide, index) in slides"
          :key="index"
          class="dot"
          :class="{ active: currentSlide === index }"
          @click="goToSlide(index)"
        ></span>
      </div>
      <button class="centered-button">Slider Button</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Sec3',
    data() {
      return {
        currentSlide: 0,
        slides: [
        { header: "Slide 1 Header", content: "s a sentence that has been used for decades as a typist's tool for practicing the keyboard. It contains all the letters of the alphabet and is a perfect example of a pangram—a sentence that uses every letter at least once. But have you ever stopped to wonder about the history behind this quirky sentence? Its origins trace back to the late 19th century when typewriters were becoming common tools. Typists needed something short, efficient, and comprehensive to practice their skills, and this sentence fit the bill perfectly. Over time, it became a" },
        { header: "Slide 2 Header", content: "s a sentence that has been used for decades as a typist's tool for practicing the keyboard. It contains all the letters of the alphabet and is a perfect example of a pangram—a sentence that uses every letter at least once. But have you ever stopped to wonder about the history behind this quirky sentence? Its origins trace back to the late 19th century when typewriters were becoming common tools. Typists needed something short, efficient, and comprehensive to practice their skills, and this sentence fit the bill perfectly. Over time, it became a" },
        { header: "Slide 3 Header", content: "s a sentence that has been used for decades as a typist's tool for practicing the keyboard. It contains all the letters of the alphabet and is a perfect example of a pangram—a sentence that uses every letter at least once. But have you ever stopped to wonder about the history behind this quirky sentence? Its origins trace back to the late 19th century when typewriters were becoming common tools. Typists needed something short, efficient, and comprehensive to practice their skills, and this sentence fit the bill perfectly. Over time, it became a" },
        { header: "Slide 4 Header", content: "s a sentence that has been used for decades as a typist's tool for practicing the keyboard. It contains all the letters of the alphabet and is a perfect example of a pangram—a sentence that uses every letter at least once. But have you ever stopped to wonder about the history behind this quirky sentence? Its origins trace back to the late 19th century when typewriters were becoming common tools. Typists needed something short, efficient, and comprehensive to practice their skills, and this sentence fit the bill perfectly. Over time, it became a" }
      ]
      };
    },
    methods: {
      nextSlide() {
        this.currentSlide = (this.currentSlide + 1) % this.slides.length;
      },
      prevSlide() {
        this.currentSlide =
          this.currentSlide === 0 ? this.slides.length - 1 : this.currentSlide - 1;
      },
      goToSlide(index) {
        this.currentSlide = index;
      }
    }
  };
  </script>
  
  <style scoped>
  .spec3-container {
    text-align: center;
    width: 100%;
    background: #ebf7fc;
    margin-top: 5%;

  }
  
  .carousel-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    max-width: 700px;
    margin: auto;
  }
  
  .slider-container {
    position: relative;
    width: 100%;
    max-width: 600px;
    margin: auto;
    overflow: hidden;
    background-color: #fff;
  }
  
  .slider {
    display: flex;
    transition: transform 0.5s ease-in-out;
    width: 100%;
  }
  
  .slider-item {
    flex: 0 0 100%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 200px; /* Adjust this value based on your content */
  }
  
  .slide-content {
    padding: 20px;
    text-align: center;
  }
  
  .arrow {
    background: #043953;
    color: white;
    border-radius: 50%;
    padding: 5px;
    width: 40px; /* Fixed width */
    height: 40px; /* Fixed height */
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    border: none;
  }
  
  .left-arrow {
    margin-right: 20px;
  }
  
  .right-arrow {
    margin-left: 20px;
  }
  
  .dots {
    text-align: center;
    margin-top: 20px;
  }
  
  .dot {
    height: 15px;
    width: 15px;
    margin: 0 5px;
    background-color: #bbb;
    border-radius: 50%;
    display: inline-block;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .dot.active {
    background-color: #01818c;
  }
  .centered-button{
    background: #043953;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  font-weight:500;
  cursor: pointer;
  margin-top:2%;
  margin-bottom:5%;
  }
  </style>