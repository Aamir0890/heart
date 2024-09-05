<template>
    <div>
      <div class="container" style="margin-bottom: 20px" v-for="category in categories" :key="category">
        <div class="dropdown" @click="toggleDropdown(category)">
          <div class="dropdown-content">
            <span class="dropdown-label">{{ category.charAt(0).toUpperCase() + category.slice(1) }}</span>
            <svg
              class="dropdown-arrow"
              :class="{ 'rotate-180': dropdownStates[category] }"
              width="29"
              height="18"
              viewBox="0 0 29 18"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M23.5483 2L15.2877 10L5.92561 2"
                stroke="#32959D"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </div>
        </div>
        <div v-if="dropdownStates[category]" class="cards-container">
          <div
            v-for="(show, index) in shows[category]"
            :key="show.id"
            class="card-wrapper"
          >
            <p class="card-top-text">{{ show.type }}</p>
            <div class="card" :style="{ borderColor: getBorderColor(index) }">
              <div class="card-content">
                <h2>{{ show.name }}</h2>
                <div class="card-details">
                  <p class="description" v-html="truncateSummary(show.summary)"></p>
                  <div class="price-divider"></div>
                  <div class="price">
                    <span>Rating: <span class="original-price">{{ show.rating.average || 'N/A' }}</span></span>
                    <span
                      class="discounted-price"
                      :style="{ color: getBorderColor(index), fontWeight: '400' }"
                    >
                      {{ show.runtime }} min
                    </span>
                  </div>
                </div>
              </div>
              <a :href="getShowLink(show)" target="_blank" rel="noopener noreferrer">
                <button
                  :style="{ backgroundColor: getBorderColor(index), borderRadius: 0 }"
                >
                  Visit Show
                </button>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, reactive, onMounted } from 'vue'
  
  export default {
    name: 'Sec2',
    setup() {
      const categories = ['cars', 'trucks', 'bands']
      const shows = reactive({
        cars: [],
        trucks: [],
        bands: []
      })
      const dropdownStates = reactive({
        cars: false,
        trucks: false,
        bands: false
      })
      const isLoading = ref(true)
  
      const fetchShows = async () => {
        for (const category of categories) {
          try {
            const response = await fetch(`https://api.tvmaze.com/search/shows?q=${category}`)
            const data = await response.json()
            shows[category] = data.slice(0, 3).map(item => item.show)
          } catch (error) {
            console.error(`Error fetching data for ${category}:`, error)
          }
        }
        isLoading.value = false
      }
  
      const toggleDropdown = (category) => {
        dropdownStates[category] = !dropdownStates[category]
      }
  
      const getBorderColor = (index) => {
        const colors = ['#2B7397', '#32959D', '#9C7777']
        return colors[index % 3]
      }
  
      const truncateSummary = (summary) => {
        if (!summary) return 'No summary available'
        const stripped = summary.replace(/<\/?[^>]+(>|$)/g, "")
        return stripped.length > 100 ? stripped.substr(0, 97) + '...' : stripped
      }
  
      const getShowLink = (show) => {
        return show.officialSite || show.url || '#'
      }
  
      onMounted(fetchShows)
  
      return {
        categories,
        shows,
        dropdownStates,
        isLoading,
        toggleDropdown,
        getBorderColor,
        truncateSummary,
        getShowLink
      }
    }
  }
  </script>
  
  <style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

  * {
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
  box-sizing: border-box;
}


  .container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction:column;
  
}

.dropdown {
  display: inline-block;
  position: relative;
  width: 50%;
}

.dropdown-content {
  display: flex;
  align-items: center;
  background-color: #e3f3f5; /* Light blue background */
  border-radius: 4px;
  padding: 8px 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.dropdown-label {
  flex: 1;
  color: #333;
  font-family: 'Roboto', sans-serif;
  font-size: 20px;
  margin-top:1%;
  
  margin-left: 16%;
}

.dropdown-arrow {
  margin-left: 8px;
  cursor: pointer;
}

.dropdown-content svg {
  vertical-align: middle;
}

.cards-container {
  display: flex;
  flex-wrap: nowrap; /* Prevent wrapping of cards */
  gap: 16px; /* Spacing between cards */
  justify-content: center;
  padding: 16px;
}

.card-wrapper {
  flex: 1 1 300px; /* Grow and shrink, with a base width of 300px */
  max-width: 300px; /* Ensure card doesn't exceed 300px */
}
.card-top-text {
  text-align: center;
  margin-bottom: 10px; /* Adjust as needed */
  font-size: 20px;
}

.card {
  border: 2px solid;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  background-color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.card-content {
  margin-bottom: 16px;
}
h2 {
  margin: 10%;
}

.card-details {
  display: flex;
  flex-direction: column;
}

.description {
  margin: 3%;

}

.price-divider {
  display: none;
}

.price {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 8px 0;
}

.original-price {
  text-decoration: line-through;
  color: #888;
}

.discounted-price {
  font-size: 20px;
  font-weight: bold;
  color: #000;
  margin-top: 20px;
}

button {
  border: none;
  color: #fff;
  padding: 10px 0;
  cursor: pointer;
  font-size: 16px;
  width: 100%;
  text-align: center;
}

@media (max-width: 600px) {
    .cards-container {
    flex-wrap: wrap; /* Allow wrapping on smaller screens */
    justify-content: space-between; /* Adjust alignment on small screens */
  }

  .card-wrapper {
    flex: 1 1 100%; /* Full width on small screens */
    max-width: none; /* Remove max-width */
  }

  .card-top-text {
    display: none; /* Hide top text on small screens */
  }
  .card-content {
    display: flex;
    flex-direction: column;
  }

  .card-details {
    flex-direction: row;
    justify-content: space-between;
    align-items: flex-start;
  }

  .description {
    margin: 5%;
    text-align: left;
    width: 60%;
  }

  .price-divider {
    display: block;
    width: 1px;
    background-color: #ccc;
    align-self: stretch;
    margin: 0 10px;
    
  }

  .price {
    margin: 5%;
    align-items: flex-start;
    width: 30%;
  }
}

  </style>
  