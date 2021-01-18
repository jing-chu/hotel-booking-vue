<template>
  <div>
    <div>{{ hotel.name }}</div>
    <div class="slider">
      <Slider
        :id="$route.params.id"
        :hotel="hotel"
        :hotelImages="hotelImages"
      />
    </div>
    <article class="hotelInfo">
      <ul>
        <li>
          <span>Name:</span>
          <p>{{ hotel.name }}</p>
        </li>
        <li>
          <span>Address:</span>
          <p>{{ hotel.address.fullAddress }}</p>
        </li>
        <li>
          <span>Star:</span>
          <p>{{ hotel.starRatingTitle }}</p>
        </li>
        <li>
          <span>Note:</span>
          <p>{{ hotel.tagline[0] }}</p>
        </li>
      </ul>
    </article>
    <div>
      <form @submit.prevent="onSubmit">
        <button type="submit">BOOKING</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Slider from "../../../components/Slider";

export default {
  components: {
    Slider,
  },

  data() {
    return {
      hotel: {},
      hotelImages: [],
    };
  },

  methods: {
    onSubmit() {
      const bookingData = {
        hotel_name: this.hotel.name,
        hotel_id: this.$route.params.id,
        room_type: "Single Room",
        persons: this.$route.query.adultsNumber,
        booking_date_from: this.$route.query.dateCheckIn,
        booking_date_until: this.$route.query.dateCheckOut,
        comments: "",
        customer_name: "",
        customer_email: "jinjing@gmail.com",
      };
      console.log(bookingData);
      axios
        .post(
          "https://ovu1b6gga2.execute-api.us-east-1.amazonaws.com/production/",
          bookingData
        )
        .then((res) => console.log(res))
        .catch((err) => console.log(err));
    },
  },

  created() {
    console.dir(this.$route);
    const options = {
      method: "GET",
      url: "https://hotels4.p.rapidapi.com/properties/get-details",
      params: {
        id: this.$route.params.id,
        locale: "en_US",
        currency: "USD",
        checkOut: "2020-01-15",
        adults1: "1",
        checkIn: "2020-01-08",
      },
      headers: {
        "x-rapidapi-key": "824c162859msh99a656af9fb4804p1d8721jsn37a5fb23576a",
        "x-rapidapi-host": "hotels4.p.rapidapi.com",
      },
    };

    axios
      .request(options)
      .then((response) => {
        this.hotel = response.data.data.body.propertyDescription;
        console.log(this.hotel);
        const options = {
          method: "GET",
          url: "https://hotels4.p.rapidapi.com/properties/get-hotel-photos",
          params: { id: this.$route.params.id },
          headers: {
            "x-rapidapi-key":
              "824c162859msh99a656af9fb4804p1d8721jsn37a5fb23576a",
            "x-rapidapi-host": "hotels4.p.rapidapi.com",
          },
        };

        return axios
          .request(options)
          .then((response) => {
            console.log(response.data.hotelImages);
            const images = response.data.hotelImages;
            const image5 = [];
            for (let i = 0; i <= 4; i++) {
              const formedArr = images[i].baseUrl.replace("{size}", "d");
              image5.push(formedArr);
            }
            this.hotelImages = image5;
            console.log(this.hotelImages);
          })
          .catch(function (error) {
            console.error(error);
          });
      })
      .catch(function (error) {
        console.error(error);
      });
  },

  head() {
    return {
      title: "Hotel informarion",
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
</style>