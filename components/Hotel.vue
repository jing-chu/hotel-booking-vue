<template>
  <nuxt-link
    :to="{
      path: '/hotels/' + id,
      query: { dateCheckIn, dateCheckOut, adultsNumber }
    }"
  >
    <div>
      <ul class="hotels-container">
        <li :key="id">
          <img :src="hotelImg" :alt="hotelName" />
          <div>
            <h4>{{ hotelName }}</h4>
            <p>{{ price }}</p>
          </div>
        </li>
      </ul>
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
    "adultsNumber"
  ]
};
</script>

<style>
.hotels-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin: 3rem auto;
}

.hotels-container li {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: var(--bg-secondary);
  padding: 1rem 2rem;
  border-radius: 0.25rem;
  text-align: left;
}

.hotels-container h4 {
  margin: 1rem 0;
}
</style>
