<template>
  <div>
    <form class="form" @submit.prevent="submitForm">
      <div>
        <label for="city">City</label>
        <input class="input" type="text" v-model="cityName" name="city" />
      </div>
      <div>
        <label for="dateFrom">Check In</label>
        <input class="input" type="date" v-model="dateCheckIn" />
      </div>
      <div>
        <label for="dateTo">Check Out</label>
        <input class="input" type="date" v-model="dateCheckOut" />
      </div>
      <div>
        <label for="city">Adults</label>
        <input
          type="number"
          class="input"
          v-model="adultsNumber"
          name="adults"
        />
      </div>

      <div>
        <button type="submit" class="btn">Search</button>
      </div>
    </form>
    <div>
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
</template>

<script>
import axios from "axios";
import Hotel from "../../components/Hotel";

export default {
  components: {
    Hotel,
  },

  data() {
    return {
      cityName: "Leuven",
      dateCheckIn: "",
      dateCheckOut: "",
      adultsNumber: 1,
      hotels: [],
    };
  },

  methods: {
    submitForm() {
      const options = {
        method: "GET",
        url: "https://hotels4.p.rapidapi.com/locations/search",
        params: { query: this.cityName, locale: "en_US" },
        headers: {
          "x-rapidapi-key":
            "25670207fbmsh89696375d639f1bp1096e1jsn690ff96fa0a6",
          "x-rapidapi-host": "hotels4.p.rapidapi.com",
        },
      };

      axios
        .request(options)
        .then((response) => {
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
              sortOrder: "PRICE",
            },
            headers: {
              "x-rapidapi-key":
                "25670207fbmsh89696375d639f1bp1096e1jsn690ff96fa0a6",
              "x-rapidapi-host": "hotels4.p.rapidapi.com",
            },
          };

          return axios
            .request(options)
            .then((response) => {
              console.log(response.data.data.body.searchResults.results);
              this.hotels = response.data.data.body.searchResults.results;
            })
            .catch(function (error) {
              console.error(error);
            });
        })
        .catch(function (error) {
          console.error(error);
        });
    },
  },

  head() {
    return {
      title: "Search Hotel",
      meta: [
        {
          hid: "hotel searching",
          nane: "hotel searching",
          content: "Best place for hotel searching",
        },
      ],
    };
  },
};
</script>

<style>
.form {
  background: #fff;
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
.form button {
  display: inline-block;
  background: #222;
  color: #fff;
  margin-top: 1rem;
  letter-spacing: 0.1rem;
  padding: 0.15rem 0.25rem;
  text-transform: capitalize;
  border-radius: 0.25rem;
  cursor: pointer;
}
</style>
