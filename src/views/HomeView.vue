<script setup>
import { ref } from 'vue'
const confettiCount = 5
const balloonCount = 3
const jeush1 = 2
const jeush2 = 2

const isPaused = ref(false);

function toggleAnimations() {
    isPaused.value = !isPaused.value
}

function generateFloatingStyle(type) {
    const x = Math.random() * 90
    const y = Math.random() * 80
    const delay = Math.random() * 5
    let duration = 2 + Math.random() * 3
    let scale = 0.5 + Math.random() * 0.5
    let floatY = -10 // default float

    if (type === 'balloon') {
        duration = 5 + Math.random() * 5
        scale = 0.7 + Math.random() * 0.5
        floatY = -50
    }
    if (type === 'confetti') {
        duration = 3 + Math.random() * 2
        scale = 0.3 + Math.random() * 0.4
        floatY = -20
    }
    if (type === 'jeush1') {
        duration = 2 + Math.random() * 2
        scale = 0.3 + Math.random() * 0.4
        floatY = -20
    }
    if (type === 'jeush2') {
        duration = 2 + Math.random() * 2
        scale = 0.3 + Math.random() * 0.4
        floatY = -20
    }

    return {
        left: `${x}%`,
        top: `${y}%`,
        animationDelay: `${delay}s`,
        animationDuration: `${duration}s`,
        transform: `scale(${scale})`,
        '--floatY': `${floatY}px`
    }
}
</script>

<template>
    <div class="home-wrapper">
        <div class="home-bg d-flex flex-column align-items-center text-white text-center p-3"
            :class="{ paused: isPaused }">
            <!-- Join Text -->
            <h1 class="join mb-3">Join us to celebrate!</h1>

            <!-- Image -->
            <img src="/images/jeush-1.webp" class="img-fluid rounded mb-3 jeush-image" alt="Jeush" />

            <!-- Name & Event -->
            <h2 class="name mb-1">Jeush</h2>
            <h3 class="having mb-3">is having his</h3>
            <h4 class="birthday mb-0">1st Birthday &</h4>
            <h4 class="christening mb-4">Christening</h4>

            <!-- Date -->
            <div class="d-flex justify-content-center mb-2 w-100">
                <div class="d-flex align-items-center gap-3">
                    <i class="bi bi-calendar-event-fill fs-2"></i>
                    <div class="text-start">
                        <p class="mb-0">Saturday, Nov 22nd 2025</p>
                        <p class="mb-0">8AM to 1PM</p>
                    </div>
                </div>
            </div>

            <!-- Location -->
            <div class="d-flex justify-content-center w-100">
                <div class="d-flex align-items-center gap-3">
                    <i class="bi bi-geo-alt-fill fs-2"></i>
                    <div class="text-start">
                        <p class="mb-0">Max's Restaurant</p>
                        <p class="mb-0">Commonwealth Batasan</p>
                    </div>
                </div>
            </div>
            <!-- Floating images -->
            <img v-for="(c, index) in confettiCount" :key="'confetti-' + index" src="/images/confetti.png"
                class="floating" :style="generateFloatingStyle('confetti')" />

            <img v-for="(b, index) in balloonCount" :key="'balloon-' + index" src="/images/balloons.png"
                class="floating" :style="generateFloatingStyle('balloon')" />

            <img v-for="(b, index) in jeush1" :key="'balloon-' + index" src="/images/jeush1.webp" class="floating"
                :style="generateFloatingStyle('jeush1')" />

            <img v-for="(b, index) in jeush2" :key="'balloon-' + index" src="/images/jeush2.webp" class="floating"
                :style="generateFloatingStyle('jeush1')" />

            <!-- Pause Button -->

            <a href="https://forms.gle/4CFuviNwvAJxqqTv9" target="_blank" class="btn btn-light mt-4 rsvp-btn">
                RSVP
            </a>


        </div>
    </div>
</template>

<style>
.home-wrapper {
    overflow: hidden;
    min-height: 100vh;
}

.home-bg {
    min-height: 100vh;
    background-image: url('/images/background.png');
    background-repeat: no-repeat;
    background-position: center top;
    position: relative;
}

/* Text styles */
.join {
    font-family: Angkor;
    font-size: 2rem;
    color: rgba(0, 164, 217, 1);
    text-shadow:
        2px 2px 0 #fff,
        -2px 2px 0 #fff,
        2px -2px 0 #fff,
        -2px -2px 0 #fff;
}

.jeush-image {
    max-width: 18rem !important;
    width: 100%;
    height: auto;
}

.rsvp-btn {
    color: rgba(0, 164, 217, 1) !important;
}

.name {
    font-family: 'Bowlby One SC', sans-serif;
    font-size: 4.5rem;
    /* reduced for mobile */
    color: rgba(0, 164, 217, 1);
    text-shadow:
        5px 5px 0 #fff,
        -5px 5px 0 #fff,
        5px -5px 0 #fff,
        -5px -5px 0 #fff;
}

.having {
    font-family: Angkor;
    font-size: 1.5rem;
    color: #fff;
}

.birthday {
    font-family: Bigshot One, sans-serif;
    font-size: 2.5rem;
    color: #fff;
}

.christening {
    font-family: Charm, sans-serif;
    font-weight: 700;
    font-size: 2.5rem;
    color: #fff;
}

/* Event info text */
p {
    font-family: Archivo Black, sans-serif;
    font-size: 1rem;
    margin: 0;
}


/* Confetti animation */
.floating {
    position: absolute;
    width: 5rem;
    /* adjust size as needed */
    height: 5rem;
    opacity: 0;
    animation-name: confetti-fade;
    animation-timing-function: ease-in-out;
    animation-iteration-count: infinite;
}

/* Pause animations */
.paused .floating {
    animation-play-state: paused !important;
}

/* Fade in & out animation */
@keyframes confetti-fade {
    0% {
        opacity: 0;
        transform: scale(var(--scale)) translateY(0);
    }

    50% {
        opacity: 1;
    }

    100% {
        opacity: 0;
        transform: scale(var(--scale)) translateY(-10px);
    }
}

/* Responsive tweaks */
@media (min-width: 768px) {
    .name {
        font-size: 6rem;
    }

    .birthday,
    .christening {
        font-size: 3rem;
    }
}
</style>
