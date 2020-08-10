<template>
    <select name="states" id="states" @change="getCities">
        <option selected value="None">Select State</option>
        <option v-for="(state, index) in states" :key="index" :value="state">{{state}}</option>
    </select>
</template>

<script>

export default {
    props: {
        states: Array,
        getCities: Function
    }
}
</script>