<template>
    <div class="countries-input">
        <select name="countries" id="countries" @change="getStates">
        <option selected value="None">Select Country</option>
        <option v-for="(country, index) in countries" :key="index" :value="country">{{country}}</option>
        </select>
    </div>
</template>

<script>

export default {
    props: {
        countries: Array,
        getStates: Function,
    }
}

</script>