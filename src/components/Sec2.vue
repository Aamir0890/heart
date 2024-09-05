
<template>
    <div style="display: flex;align-items: center;justify-content: center;margin-top: 15px">
    <h1 style="color:#01818C;font-weight: 500">SECTION 2 [20 points]</h1>
  </div>
  <div class="container">
    <div class="dropdown">
      <div class="dropdown-content">
        <span class="dropdown-label">Loream epsum dollar sit amet</span>
        <svg class="dropdown-arrow" width="29" height="18" viewBox="0 0 29 18" fill="none" xmlns="http://www.w3.org/2000/svg">
          <g filter="url(#filter0_d_6_1510)">
            <path d="M23.5483 10L15.2877 2L5.92561 10" stroke="#32959D" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </g>
          <defs>
            <filter id="filter0_d_6_1510" x="0.925537" y="0" width="27.6228" height="18" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="3"/>
              <feGaussianBlur stdDeviation="2"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_6_1510"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_6_1510" result="shape"/>
            </filter>
          </defs>
        </svg>
      </div>
    </div>
  </div>
  <div class="cards-container">
    <div v-for="(show,index) in shows" :key="show.id" class="card-wrapper">
      <p class="card-top-text">{{ show.type }}</p>
      <div class="card" :style="{ borderColor: getBorderColor(index) }">
        <div class="card-content">
          <h2>{{ show.name }}</h2>
          <div class="card-details">
            <p class="description" v-html="truncateSummary(show.summary)"></p>
            <div class="price-divider"></div>
            <div class="price">
              <span>Rating: <span class="original-price">{{ show.rating.average || 'N/A' }}</span></span>
              <span class="discounted-price" :style="{ color: getBorderColor(index), fontWeight: '400' }">
                {{ show.runtime }} min
              </span>
            </div>
          </div>
        </div>
        <a :href="getShowLink(show)" target="_blank" rel="noopener noreferrer">
          <button :style="{ backgroundColor: getBorderColor(index), borderRadius: 0 }">
            Visit Show
          </button>
        </a>
      </div>
    </div>
  </div>
  <div class="container" style="margin-bottom:20px">
    <div class="dropdown">
      <div class="dropdown-content">
        <span class="dropdown-label">Loream epsum dollar sit amet</span>
        <svg width="29" height="18" viewBox="0 0 29 18" fill="none" xmlns="http://www.w3.org/2000/svg">
<g filter="url(#filter0_d_6_1511)">
<path d="M23.5483 2L15.2877 10L5.92561 2" stroke="#32959D" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
</g>
<defs>
<filter id="filter0_d_6_1511" x="0.925537" y="0" width="27.6228" height="18" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
<feFlood flood-opacity="0" result="BackgroundImageFix"/>
<feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
<feOffset dy="3"/>
<feGaussianBlur stdDeviation="2"/>
<feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
<feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_6_1511"/>
<feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_6_1511" result="shape"/>
</filter>
</defs>
</svg>

      </div>
    </div>
  </div>
  <div class="container">
    <div class="dropdown">
      <div class="dropdown-content">
        <span class="dropdown-label">Loream epsum dollar sit amet</span>
        <svg width="29" height="18" viewBox="0 0 29 18" fill="none" xmlns="http://www.w3.org/2000/svg">
<g filter="url(#filter0_d_6_1511)">
<path d="M23.5483 2L15.2877 10L5.92561 2" stroke="#32959D" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
</g>
<defs>
<filter id="filter0_d_6_1511" x="0.925537" y="0" width="27.6228" height="18" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
<feFlood flood-opacity="0" result="BackgroundImageFix"/>
<feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
<feOffset dy="3"/>
<feGaussianBlur stdDeviation="2"/>
<feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
<feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_6_1511"/>
<feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_6_1511" result="shape"/>
</filter>
</defs>
</svg>

      </div>
    </div>
  </div>
  </template>
  
  <script>
  export default {
    name: 'Sec2',
    props: {
      message: {
        type: String,
        required: true
      }
    },
    data() {
    return {
      shows: []
    }
  },
  mounted() {
    this.fetchShows();
  },
  methods: {
    async fetchShows() {
     
      const queries = ['cars', 'truck', 'band'];
const newShows = [];

for (let i = 0; i < queries.length; i++) {
  try {
    const response = await fetch(`https://api.tvmaze.com/search/shows?q=${queries[i]}`);
    const data = await response.json();
    newShows.push(...data.slice(0, 3).map(item => item.show));
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}

      this.shows = newShows;
    },
    getBorderColor(index) {
  const colors = ['#2B7397', '#32959D', '#9C7777'];
  return colors[index % 3];
},
    truncateSummary(summary) {
      if (!summary) return 'No summary available';
      const stripped = summary.replace(/<\/?[^>]+(>|$)/g, "");
      return stripped.length > 100 ? stripped.substr(0, 97) + '...' : stripped;
    },
    getShowLink(show) {
      return show.officialSite || show.url || '#';
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
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
  padding: 16px;
}

.card-wrapper {
  width: 300px;
  margin: 30px;
}

.card-top-text {
  text-align: center;
  margin-bottom: 30px;
  font-size:20px;
  
}

.card {
  border: 2px solid;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  box-sizing: border-box;
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
  height:30%;
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
  .card-wrapper {
    width: 100%;
  }
  .card-top-text {
    display: none; /* Hide the top text on small screens */
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
  