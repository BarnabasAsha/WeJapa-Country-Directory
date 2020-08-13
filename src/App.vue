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
      cities: []
    }
  },
  methods: {
    getStates(e) {
     fetch(`https://www.universal-tutorial.com/api/states/${e.target.value}`, {
      method: 'get',
      headers: {
        'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7InVzZXJfZW1haWwiOiJiYXJuYWJlZTU4QGdtYWlsLmNvbSIsImFwaV90b2tlbiI6ImVWYTdjb1ZKSnpXaGtHb25LNjBibUJTR29ReHM3ajgwSllGbVZMcVNoVmhXa3Mwa24tb2ZsMndWMjJSb3drTlpkZWMifSwiZXhwIjoxNTk3NDQyMDQwfQ.PVOnLxttkHbsFHqYpgZPVLqX3aYgPwXp3pWKQBRyU0E',
        'Accept': 'application/json',
      }
    })
    .then(res => {
      return res.json()
    }).then(data => {
      this.states = data.map(state => {
        return state.state_name;
      })
    })

    },
    async getCities(e) {
    await fetch(`https://www.universal-tutorial.com/api/cities/${e.target.value}`, {
      method: 'get',
      headers: {
        'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7InVzZXJfZW1haWwiOiJiYXJuYWJlZTU4QGdtYWlsLmNvbSIsImFwaV90b2tlbiI6ImVWYTdjb1ZKSnpXaGtHb25LNjBibUJTR29ReHM3ajgwSllGbVZMcVNoVmhXa3Mwa24tb2ZsMndWMjJSb3drTlpkZWMifSwiZXhwIjoxNTk3NDQyMDQwfQ.PVOnLxttkHbsFHqYpgZPVLqX3aYgPwXp3pWKQBRyU0E',
        'Accept': 'application/json',
      }
    })
    .then(res => {
      return res.json()
    }).then(data => {
      this.cities = data.map(city => {
        return city.city_name;
      })
    })
    },
  },

  mounted: function() {
    fetch('https://www.universal-tutorial.com/api/countries/', {
      method: 'get',
      headers: {
        'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7InVzZXJfZW1haWwiOiJiYXJuYWJlZTU4QGdtYWlsLmNvbSIsImFwaV90b2tlbiI6ImVWYTdjb1ZKSnpXaGtHb25LNjBibUJTR29ReHM3ajgwSllGbVZMcVNoVmhXa3Mwa24tb2ZsMndWMjJSb3drTlpkZWMifSwiZXhwIjoxNTk3NDQyMDQwfQ.PVOnLxttkHbsFHqYpgZPVLqX3aYgPwXp3pWKQBRyU0E',
        'Accept': 'application/json',
      }
    })
    .then((res) => {
      return res.json()
    })
    .then(data => {
      this.countries = data.map(country => {
          return country.country_name;
      });
    })
  }
}
</script>

<style>
#app {
  box-sizing: border-box;
  width: 100%;
  background: #FBFBFB;
  color: #000080;
  height: 100vh;
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
  border: 1px solid #000080;
}

option {
    font-weight: normal;
    display: block;
    white-space: pre;
    min-height: 1.2em;
    padding: 0px 2px 1px;
}
</style>
