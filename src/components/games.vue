<template>
  <div class="container">
    <h3>Games</h3>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Name</th>
          <th scope="col">Year</th>
          <th scope="col">Played</th>
          <th scope="col">interested</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="game in games" v-bind:key="game.id">
          <th scope="row">{{ game.name }}</th>
          <td>{{game.releasedAt}}</td>
          <td>{{game.hasPlayed}}</td>
          <td>{{game.isInteresting}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import axios from 'axios';

  function getRow (row, id) {
    return {
      id: id,
      name: row[0],
      releasedAt: row[1],
      hasPlayed: row[3],
      isInteresting: row[4],
      isChecked: row[5],
      shouldPlayAgain: row[6],
      notes: row[8]
    }
  }

  function process (data) {
    // init
    const rows = data.values || [];

    // processing
    const response = rows.map(getRow);

    // response
    return response;
  }

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
        this.games = process(res.data);
      })
  }
}
</script>

<style>
  h3 {
    margin-bottom: 5%;
  }
</style>
