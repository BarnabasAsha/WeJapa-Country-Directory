<template>
  <div id="app">
    <Header />
    <div class="main">
      <Countries 
      :countries = "countries"
      :getStates = "getStates"
      />
      
      <States 
      :states = "states"
      :getCities = "getCities"
      />
      <Cities
      :cities = "cities" 
      />
    </div>
  </div>
</template>

<script>
 
import Header from './components/Header'
import Countries from './components/countries'
import States from './components/states'
import Cities from './components/cities'

export default {
  name: 'App',
  components: {
    Header,
    Countries,
    States,
    Cities
  },
  data() {
    return {
      countries: [],
      states: [],
      cities: [],
      currentCountry: ''
    }
  },
  methods: {
    async getStates(e) {
     await fetch(`https://cors-anywhere.herokuapp.com/http://allcountries.us-east-2.elasticbeanstalk.com/countries/details/${e.target.value}`)
    .then(res => {
      return res.json()
    }).then(data => {
        this.states = data.states.map(state => {
        return state.name;
      })
      })
      this.currentCountry = e.target.value
    },
    async getCities(e) {
    await fetch(`https://cors-anywhere.herokuapp.com/http://allcountries.us-east-2.elasticbeanstalk.com/countries/details/${this.currentCountry}`)
    .then(res => {
      return res.json()
    }).then(data => {
        data.states.forEach(state => {
        if(state.name == e.target.value){
        const cities = state.cities
        this.cities = [...cities.map(city => { return city.name })]
        } 
      })
    })    
    },
  },

  mounted: function() {
  fetch('https://cors-anywhere.herokuapp.com/http://allcountries.us-east-2.elasticbeanstalk.com/countries/list')
    .then((res) => {
      return res.json()
    })
    .then(data => {
      this.countries = data;
      });
  }
}
</script>

<style>
body {
  background: #1D3557;
}
#app {
  box-sizing: border-box;
  width: 100%;
  color: #A8DADC;
  height: 100vh;
  padding: 2em;
}

.main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 3em;
}


select {
  width: 300px;
  padding: 10px 10px;
  margin: 0.5em 0;
  border-radius: 5px;
  border: 2px solid #A8DADC;
  background: #f1f0f0;
  color: #1D3557;
}

option {
    font-weight: normal;
    display: block;
    white-space: pre;
    min-height: 1.2em;
    padding: 0px 2px 1px;
    background: #f1f0f0;
    color: #1D3557;
}
</style>
