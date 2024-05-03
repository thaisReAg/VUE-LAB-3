<script setup>
import { ref, computed, watch } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();

const country = ref(null);

const countryCode = computed(() => {
  return route.params.alpha3Code;
});

const getCountryByAlphaCode = async () => {
  const alpha3Code = route.params.alpha3Code;

  const response = await fetch(`https://ih-countries-api.herokuapp.com/countries/${alpha3Code}`);

  const finalResponse = await response.json();

  country.value = finalResponse;
};
getCountryByAlphaCode();

watch(countryCode, (newCountryCode) => {
  getCountryByAlphaCode();
});
</script>

<template>
  <section v-if="country">
    <div class="col-7">
      <img
        src="https://restcountries.eu/data/fra.svg"
        alt="country flag"
        style="width: 300px" />
      <h1>{{ country.name.common }}</h1>
      <table class="table">
        <thead></thead>
        <tbody>
          <tr>
            <td style="width: 30%">Capital</td>
            <td>{{ country.capital }}</td>
          </tr>
          <tr>
            <td>Area</td>
            <td>{{ country.area }} km <sup>2</sup></td>
          </tr>
          <tr>
            <td>Borders</td>
            <td>
              <ul>
                <li
                  v-for="border in country.borders"
                  :key="border">
                  {{ border }}
                </li>
              </ul>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>
</template>

<style scoped></style>
