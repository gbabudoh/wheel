<template>
    <div class="spinner-container">
      <!-- Title -->
      <h1 class="title">Chromatic Dynamics</h1>
  
      <!-- Spinning and Color-Changing Wheel -->
      <div class="wheel" :class="{ spinning: isSpinning }">
        <div
          v-for="(ball, index) in balls"
          :key="index"
          class="ball"
          :style="{
            backgroundColor: ball.color,
            top: ball.position.y + 'px',
            left: ball.position.x + 'px',
            animationDelay: ball.delay + 's',
          }"
        ></div>
      </div>
  
      <!-- Controls -->
      <div class="controls">
        <button class="action-button" @click="showBalls">Spin</button>
        <button class="action-button" @click="resetWheel">Reset</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        balls: [], // Array to hold ball data
        isSpinning: false, // Indicates if the wheel is spinning
        wheelSize: 400, // Diameter of the wheel
        ballSize: 30, // Size of each ball
        colors: [
          "yellow",
          "green",
          "blue",
          "pink",
          "purple",
          "red",
          "black",
          "orange",
          "brown",
          "teal",
          "lime",
          "cyan",
          "magenta",
          "gold",
          "silver",
          "navy",
          "maroon",
          "olive",
        ], // Array of colors for the balls
      };
    },
    methods: {
      showBalls() {
        if (this.balls.length > 0 || this.isSpinning) return; // Prevent re-triggering
  
        this.isSpinning = true; // Start spinning the wheel
  
        const totalBalls = 50; // Total number of balls
        const radius = (this.wheelSize - this.ballSize) / 2; // Radius for positioning balls inside the wheel
  
        // Generate balls with unique positions and random colors
        this.balls = Array.from({ length: totalBalls }, () => ({
          color: this.colors[Math.floor(Math.random() * this.colors.length)], // Random color
          position: this.getRandomPosition(radius), // Random position
          delay: Math.random() * 2, // Random animation delay for staggered movement
        }));
      },
      resetWheel() {
        this.balls = []; // Clear the balls
        this.isSpinning = false; // Stop spinning the wheel
      },
      getRandomPosition(radius) {
        // Generate random coordinates within a circle
        let angle = Math.random() * 2 * Math.PI; // Random angle
        let distance = Math.random() * radius; // Random distance from center
        return {
          x: Math.cos(angle) * distance + radius, // X coordinate
          y: Math.sin(angle) * distance + radius, // Y coordinate
        };
      },
    },
  };
  </script>
  
  <style scoped>
  /* Spinner container */
  .spinner-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
  }
  
  /* Title styling */
  .title {
    font-size: 28px;
    font-weight: bold;
    margin-bottom: 20px;
    color: #333;
    text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);
  }
  
  /* Wheel styling */
  .wheel {
    width: 400px;
    height: 400px;
    border: 10px solid transparent;
    border-radius: 50%;
    position: relative;
    overflow: hidden;
    background-color: #f8f9fa;
    display: flex;
    justify-content: center;
    align-items: center;
    background-clip: padding-box;
    box-shadow: 0 0 0 10px transparent;
  }
  
  /* Add spinning and color-changing border effect */
  .wheel.spinning {
    animation: spin 5s linear infinite, colorChangeBorder 5s linear infinite;
  }
  
  /* Ball styling */
  .ball {
    position: absolute;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    animation: scatter 5s infinite; /* Independent scatter animation */
  }
  
  /* Controls styling */
  .controls {
    display: flex;
    gap: 20px;
  }
  
  .action-button {
    width: 120px; /* Fixed width */
    height: 50px; /* Fixed height */
    padding: 0; /* Remove default padding */
    font-size: 16px;
    font-weight: bold;
    color: white;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .action-button:first-of-type {
    background-color: #28a745; /* Spin button color */
    border: 2px solid;
  }
  
  .action-button:first-of-type:hover {
    background-color: #218838;
  }
  
  .action-button:last-of-type {
    background-color: #dc3545; /* Reset button color */
    border: 2px solid;
  }
  
  .action-button:last-of-type:hover {
    background-color: #a71d2a;
  }
  
  /* Ball scatter animation */
  @keyframes scatter {
    0% {
      transform: translate(0, 0);
    }
    25% {
      transform: translate(40px, -40px);
    }
    50% {
      transform: translate(-40px, 40px);
    }
    75% {
      transform: translate(-40px, -40px);
    }
    100% {
      transform: translate(0, 0);
    }
  }
  
  /* Wheel spinning animation */
  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  
  /* Wheel border color-changing animation */
  @keyframes colorChangeBorder {
    0% {
      box-shadow: 0 0 0 10px #f0c85c;
    }
    25% {
      box-shadow: 0 0 0 10px #73eaf7;
    }
    50% {
      box-shadow: 0 0 0 10px #498c64;
    }
    75% {
      box-shadow: 0 0 0 10px #d5aa9c;
    }
    100% {
      box-shadow: 0 0 0 10px #3b127e;
    }
  }
  </style>
  