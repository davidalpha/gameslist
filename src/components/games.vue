<template>
  <h3>Games:</h3>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'games',
    data() {
      return {
        games: null
    };
  },

  created: function() {
    axios
      .get('https://sheets.googleapis.com/v4/spreadsheets/1KlxXzRMWO3MdSEoQANpTuJOfFZ9iOiYtoPCxN9qc6CM/values/Sheet1?key=AIzaSyAOYzRf8SZJi4y7kaqYP8zSQ9orD1rJLyA')
      .then(res => {
        this.games = res.data;
      })
  }
}
</script>

<style>
  h3 {
    margin-bottom: 5%;
  }
</style>
