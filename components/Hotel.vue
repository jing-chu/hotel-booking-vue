<template>
  <nuxt-link
    :to="{
      path: '/hotels/' + id,
      query: { dateCheckIn, dateCheckOut, adultsNumber },
    }"
  >
    <div>
      <ul class="hotels"></ul>
      <li>
        <img :src="hotelImg" :alt="hotelName" />
        <div>
          <h4>{{ hotelName }}</h4>
          <p>{{ price }}</p>
        </div>
      </li>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: "Hotel",
  props: [
    "id",
    "hotelName",
    "hotelImg",
    "price",
    "dateCheckIn",
    "dateCheckOut",
    "adultsNumber",
  ],
};
</script>

<style>
.hotels {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin: 3rem auto;
}
.hotels li {
  width: 100%;
  display: flex;
  align-items: center;
  background: #fff;
  padding: 1rem 2rem;
  border-radius: 0.25rem;
  text-align: left;
}
.hotels img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 1rem;
}
.hotels h4 {
  margin-bottom: 0.15rem;
}
</style>
