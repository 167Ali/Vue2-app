<template>
    <div class="detail-view">
        <!-- Background Video -->
        <video class="background-video" autoplay loop muted>
            <source src="@/assets/3194277-hd_1920_1080_30fps.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
        <!-- Audio Soundtrack -->
        <audio autoplay loop>
            <source src="@/assets/interstellar.mp3" type="audio/mpeg">
            Your browser does not support the audio tag.
        </audio>
        <!-- Foreground Content -->
        <router-link to="/userdata" class="back-button"><i class="fa fa-arrow-left"></i></router-link>
        <div class="content">
            <h1 class="title">{{ title }}</h1>
            <img :src="url" alt="NASA Image" class="detail-image"/>
            <p class="explanation">{{ explanation }}</p>
            <small class="date">📅 {{ date }}</small>
        </div>
    </div>
</template>

<script>
export default {
    props: ['url', 'title', 'explanation', 'date'] // Receive data as props
};
</script>

<style scoped>
.detail-view {
    position: relative;
    overflow: hidden;
    height: 100vh;
    color: white; /* Ensure text is visible on the video background */
}

.background-video {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: -1; /* Place behind other content */
    filter: brightness(0.5); /* Darken video for better text readability */
}

.content {
    position: relative; /* Ensure content is above video */
    z-index: 1; /* Place above video */
    background: rgba(255, 255, 255, 0.8); /* Slightly transparent background for readability */
    border-radius: 8px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
    padding: 20px;
    max-width: 600px;
    margin: 20px auto;
    width: 100%;
    box-sizing: border-box;
    animation: bounceIn 1s ease-out;
    animation: slideUp 1s ease-out;
    max-height: 780px;
    overflow: auto;
}

.back-button {
    position: absolute;
    top: 20px;
    left: 20px;
    background-color: #4c8890;
    color: white;
    border: none;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: background-color 0.3s;
    text-decoration: none;
}

.back-button:hover {
    background-color: #9bdaea;
}



.title {
    font-size: 2rem;
    margin: 0 0 15px;
    color: #333;
}

.detail-image {
    width: 100%; /* Ensure the image takes the full width of the container */
    height: auto; /* Maintain aspect ratio */
    max-height: 400px; /* Set a maximum height to keep it from being too tall */
    object-fit: cover; /* Cover the area while maintaining aspect ratio */
    border-radius: 8px; /* Rounded corners */
    margin-bottom: 15px; /* Space below the image */
}

.explanation {
    font-size: 1rem;
    line-height: 1.5;
    color: #555;
}

.date {
    font-size: 0.9rem;
    color: #777;
}
.detail-view {
    animation: fadeIn 1s ease-out;
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
.detail-image {
    transition: transform 0.3s ease;
}

.detail-image:hover {
    transform: scale(1.05);
}

@keyframes slideUp {
    from {
        transform: translateY(20px);
        opacity: 0;
    }
    to {
        transform: translateY(0);
        opacity: 1;
    }
}
.back-button {
    transition: background-color 0.3s, box-shadow 0.3s, transform 0.3s;
}

.back-button:hover {
    background-color: #9bdaea;
    box-shadow: 0 6px 8px rgba(0, 0, 0, 0.2);
    transform: scale(1.1);
}

@keyframes bounceIn {
    0% {
        transform: scale(0.5);
        opacity: 0;
    }
    60% {
        transform: scale(1.1);
        opacity: 1;
    }
    100% {
        transform: scale(1);
        opacity: 1;
    }
}

</style>