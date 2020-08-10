<template>
    <select name="cities" id="cities">
        <option selected value="None">Select City</option>
        <option v-for="(city, index) in cities" :key="index" :value="city">{{city}}</option>
    </select>
</template>

<script>
export default {
    props: {
        cities: Array,
    }
}
</script>