<template>
    <div class="container">
        <!-- Background Video -->
        <video class="background-video" autoplay loop muted>
            <source src="@/assets/card_bg.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

        <!-- Audio Soundtrack -->
        <audio autoplay loop>
            <source src="@/assets/interstellar.mp3" type="audio/mpeg">
            Your browser does not support the audio tag.
        </audio>


        <!-- Content -->
        <router-link to="/dashboard" class="back-button"><i class="fa fa-arrow-left"></i></router-link>
        <h1 class="text-center mt-3 mb-5">🚀 NASA Astronomy Pictures</h1>

        <!-- Loading Spinner -->
        <div v-if="loading">
            <div class="spinner-border" role="status">
                <span class="sr-only">Loading...</span>
            </div>
        </div>

        <!-- Cards for NASA Data -->
        <v-container v-if="!loading && paginatedData.length" fluid>
            <v-row>
                <v-col v-for="(item, index) in paginatedData" :key="index" cols="12" sm="6" md="4" lg="4">
                    <v-card @click="goToDetail(item)" class="card">
                        <!-- Image Section -->
                        <v-img :src="item.url" alt="NASA Astronomy Image" aspect-ratio="1.7" />

                        <!-- Card Content -->
                        <v-card-title class="single-line-title">
                            {{ item.title }}
                          </v-card-title>

                       
                    </v-card>
                </v-col>
            </v-row>
        </v-container>

        <!-- Pagination Controls -->
        <nav aria-label="Page navigation" class="mt-4">
            <ul class="pagination justify-content-center custom-pagination">
                <li class="page-item" :class="{ disabled: currentPage === 1 }">
                    <button class="page-link" @click="prevPage" aria-label="Previous">
                        &#8592; <!-- Left arrow -->
                    </button>
                </li>
                <li class="page-item" :class="{ disabled: currentPage === totalPages }">
                    <button class="page-link" @click="nextPage" aria-label="Next">
                        &#8594; <!-- Right arrow -->
                    </button>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
    data() {
        return {
            currentPage: 1,  // Make sure currentPage is defined here
            itemsPerPage: 6, // Number of items per page
        };
    },
    computed: {
        ...mapState(['nasaData', 'loading']),
        totalPages() {
            return Math.ceil(this.nasaData.length / this.itemsPerPage);
        },
        paginatedData() {
            const start = (this.currentPage - 1) * this.itemsPerPage;
            const end = start + this.itemsPerPage;
            return this.nasaData.slice(start, end);
        },
    },
    created() {
        // Fetch data only if it's not already loaded
        if (this.nasaData.length === 0) {
            this.$store.dispatch('fetchNASAData');
        }
    },
    methods: {
        nextPage() {
            if (this.currentPage < this.totalPages) {
                this.currentPage += 1;
            }
        },
        prevPage() {
            if (this.currentPage > 1) {
                this.currentPage -= 1;
            }
        },
        truncateText(text, maxLength) {
            return text.length > maxLength ? text.substring(0, maxLength) + '...' : text;
        },
        goToDetail(item) {
            if (item && item.date) {
                this.$router.push({ path: `/detail/${item.date}`, query: { url: item.url, title: item.title, explanation: item.explanation, date: item.date } });
            } else {
                console.error('Item or item.date is undefined:', item);
            }
        }
    }
};
</script>
<style scoped>
.container {
    position: relative;
    /* Allows absolute positioning of children */
    max-width: 1200px;
    margin: auto;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    z-index: 1;
    /* Ensure content is above the video */
}

/* Background Video Styling */
.background-video {
    position: fixed;
    /* Absolute positioning to cover the background */
    top: 0;
    left: 0;
    width: 100vw;
    /* Full viewport width */
    height: 100vh;
    /* Full viewport height */
    object-fit: cover;
    /* Cover the entire viewport without distortion */
    z-index: -1;
    /* Place the video behind the content */
    pointer-events: none;
    /* Ensures the video doesn't block interactions */
}

.card-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
}

.card {
    width: 100%;
    max-width: 350px;
    background: #fff;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 300px;
    margin-top: 10px;
}

.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 25px rgba(0, 0, 0, 0.2);
}

/* Card Image Styling */
.card-image img {
    width: 100%;
    height: 150px;
    object-fit: cover;
}
.single-line-title {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    box-sizing: border-box;
    display: block;
  }
/* Card Content */
.card-content {
    padding: 10px;
}

.card-title {
    font-size: 1rem;
    font-weight: bold;
    margin-bottom: 5px;
    color: #333;
}



/* Card Footer */
.card-footer {
    padding: 10px 10px;
    background-color: #f9f9f9;
    text-align: right;
    font-size: 0.75rem;
    color: #777;
}

/* Pagination Styling */
.custom-pagination {
    margin-top: 15px;
    display: flex;
    /* Display items in a horizontal row */
    justify-content: center;
    /* Center the pagination controls */
    list-style-type: none;
    /* Remove bullet points */
    padding: 0;
}

.custom-pagination .page-item {
    margin: 0 10px;
    /* Add horizontal spacing between buttons */
}

.custom-pagination .page-link {
    padding: 8px 16px;
    border-radius: 25px;
    background-color: #f8f9fa;
    border: 1px solid #dee2e6;
    color: #007bff;
    transition: background-color 0.3s, box-shadow 0.3s;
    text-decoration: none;
}

.custom-pagination .page-link:hover {
    background-color: #6ce9f6;
    color: white;
    box-shadow: 0 4px 10px rgba(0, 123, 255, 0.3);
}

.spinner-border {
    width: 3rem;
    height: 3rem;
}

h1 {
    font-size: 2.5rem;
    color: rgb(0, 0, 0);
}

.spinner-border {
    width: 3rem;
    height: 3rem;
    border: 0.25em solid transparent;
    /* Base border */
    border-top-color: #007bff;
    /* Spinner color */
    border-radius: 50%;
    /* Make it circular */
    animation: spin 1s linear infinite;
    /* Spin animation */
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}

.spinner-border {
    border-top-color: #28a745;
    /* Green color */
}

/* Style for the Back Button */
.back-button {
    position: fixed;
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
    text-decoration: none;
    cursor: pointer;
    transition: background-color 0.3s, box-shadow 0.3s;
}

.back-button:hover {
    background-color: #9bdaea;
    box-shadow: 0 6px 8px rgba(0, 0, 0, 0.2);
}

.back-button i {
    font-size: 18px;
}

@media (max-width: 768px) {
    h1 {
        font-size: 2rem;
        /* Smaller font size for tablets */
    }
}

@media (max-width: 576px) {
    h1 {
        font-size: 1.5rem;
        /* Even smaller font size for mobile */
    }
}
</style>