<template>
  <form @submit.prevent="getWeather">
    <div>
      <label>city</label>
      <input v-model.trim="city" />
    </div>
    <button type="submit">get weather</button>
  </form>
  <div>
    <p>feels like: {{ result.feels_like }}</p>
    <p>humidity: {{ result.humidity }}</p>
    <p>pressure: {{ result.pressure }}</p>
    <p>temperature: {{ result.temp }}</p>
    <p>high: {{ result.temp_max }}</p>
    <p>low: {{ result.temp_min }}</p>
  </div>
</template>
<script>
const APIKEY = "your-api-key";
export default {
  name: "App",
  data() {
    return {
      city: "",
      result: {},
    };
  },
  methods: {
    async getWeather() {
      if (!this.city) {
        return;
      }
      const res = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${APIKEY}`
      );
      const { main } = await res.json();
      this.result = main;
    },
  },
};
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
