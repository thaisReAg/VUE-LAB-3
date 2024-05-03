<script setup>
const props = defineProps(
  {countries: Array}
)

</script>

<template>
  <section class="flex">
  <ul>
    <li v-for="(country, index) in countries" :key="index">
      <RouterLink :to="`/list/${country.alpha3Code}`">{{country.name.common}}</RouterLink>
    </li>
  </ul>
  <router-view></router-view>
</section>
</template>

<style scoped>
.flex{
  display: flex;
}
</style>