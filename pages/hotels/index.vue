<template>
  <div>
    <div class="main-container">
      <div>
        <form class="form" @submit.prevent="submitForm">
          <div class="form-control">
            <label for="city">City *</label>
            <input
              class="input"
              type="text"
              v-model="cityName"
              name="city"
              placeholder="Leuven"
            />
          </div>
          <div class="form-control">
            <label for="dateFrom">Check In *</label>
            <input class="input" type="date" v-model="dateCheckIn" />
          </div>
          <div class="form-control">
            <label for="dateTo">Check Out *</label>
            <input class="input" type="date" v-model="dateCheckOut" />
          </div>
          <div class="form-control">
            <label for="city">Adults *</label>
            <input
              type="number"
              class="input"
              v-model="adultsNumber"
              name="adults"
              placeholder="0"
            />
          </div>
          <div>
            <button type="submit" class="btn">Search</button>
          </div>
        </form>
      </div>
      <div>
        <p class="loading" v-if="isLoading">Loading...</p>
        <div v-else>
          <Hotel
            v-for="hotel in hotels"
            :key="hotel.id"
            :id="hotel.id"
            :hotelName="hotel.name"
            :hotelImg="hotel.thumbnailUrl"
            :price="hotel.ratePlan.price.current"
            :dateCheckIn="dateCheckIn"
            :dateCheckOut="dateCheckOut"
            :adultsNumber="adultsNumber"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Hotel from "../../components/Hotel";

export default {
  components: {
    Hotel
  },

  data() {
    return {
      cityName: "",
      dateCheckIn: "",
      dateCheckOut: "",
      adultsNumber: 0,
      hotels: [],
      isLoading: false
    };
  },

  methods: {
    submitForm() {
      if (
        (this.cityName, this.dateCheckIn, this.dateCheckOut, this.adultsNumber)
      ) {
        this.isLoading = true;
        const options = {
          method: "GET",
          url: "https://hotels4.p.rapidapi.com/locations/search",
          params: { query: this.cityName, locale: "en_US" },
          headers: {
            "x-rapidapi-key":
              "25670207fbmsh89696375d639f1bp1096e1jsn690ff96fa0a6",
            "x-rapidapi-host": "hotels4.p.rapidapi.com"
          }
        };

        axios
          .request(options)
          .then(response => {
            console.log(response.data);
            const destinationId =
              response.data.suggestions[0].entities[0].destinationId;
            console.log(destinationId);

            const options = {
              method: "GET",
              url: "https://hotels4.p.rapidapi.com/properties/list",
              params: {
                destinationId: destinationId,
                pageNumber: "1",
                checkIn: this.dateCheckIn,
                checkOut: this.dateCheckOut,
                pageSize: "25",
                adults1: this.adultsNumber,
                currency: "USD",
                locale: "en_US",
                sortOrder: "PRICE"
              },
              headers: {
                "x-rapidapi-key":
                  "25670207fbmsh89696375d639f1bp1096e1jsn690ff96fa0a6",
                "x-rapidapi-host": "hotels4.p.rapidapi.com"
              }
            };

            return axios
              .request(options)
              .then(response => {
                this.isLoading = false;
                console.log(response.data.data.body.searchResults.results);
                this.hotels = response.data.data.body.searchResults.results;
              })
              .catch(function(error) {
                console.error(error);
              });
          })
          .catch(function(error) {
            console.error(error);
          });
      } else {
        alert("filds with * are necessary");
      }
    }
  },

  head() {
    return {
      title: "Search Hotel",
      meta: [
        {
          hid: "hotel searching and booking",
          nane: "hotel searching and booking",
          content: "Best place for hotel searching and booking"
        }
      ]
    };
  }
};
</script>

<style>
.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 1rem;
}

.form {
  background: var(--bg);
  max-width: 450px;
  margin: 0 auto;
  margin-bottom: 4rem;
  padding: 1rem 2rem;
  border-radius: 0.25rem;
}
.form input {
  background: hsl(210, 36%, 96%);
  border-color: transparent;
  border-radius: 0.25rem;
  padding: 0.25rem 0.5rem;
}
.form-control {
  margin: 0.5rem 0;
  display: grid;
  grid-template-columns: 100px 1fr;
  align-items: center;
}
.form button {
  display: inline-block;
  background: #333;
  color: #fff;
  border-color: transparent;
  margin-top: 1rem;
  text-transform: capitalize;
  border-radius: 0.25rem;
  cursor: pointer;
  border-radius: 0.25rem;
  padding: 0.3rem 1rem;
}
</style>
