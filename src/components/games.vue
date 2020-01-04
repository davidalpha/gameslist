<template>
<div class="container">
  <div class="mx-auto" style="width: 500px;">
    <div class="form-group row">
      <div class="Filter">
        <select class="form-control" id="sel1" v-model="filteredProperty">
          <option value="name">Name</option>
          <option value="releasedAt">year</option>
          <option value="shouldPlayAgain">Play again?</option>
        </select>
      </div>
    <div class="col-xs-3">
      <input class="form-control" placeholder="..." v-model="query">
    </div>
      <button class="btn btn-primary btn-sm" @click="addFilter()">add filter</button>
    </div>
  </div>

  <hr>
  <table class=".table-striped" v-if="activeFilters.length">
    <tr style="width: 100px">
      <th colspan="3">Filters in use:</th>
    </tr>
    <tr v-for="(filter, index) in activeFilters" :key="index">
      <td>{{ filter.name }}:</td>
      <td>{{ filter.value }}</td>
      <td style="padding-left: 10px;">
        <a class="btn btn-warning btn-sm" role="button" href="#" @click="removeFilter(index)">
          remove
        </a>
      </td>
    </tr>
  </table>
  <hr v-if="activeFilters.length">
  <table class="table-striped">
    <tbody>
      <th>Name</th>
      <th>Year</th>
      <th>Recommended</th>
      <tr v-for="(record, index) in filtered" :key="index">
        <td style="padding-right:18px;">{{ record.name }}</td>
        <td style="padding-right:18px;">{{ record.releasedAt }}</td>
        <td>{{ record.shouldPlayAgain }}</td>
      </tr>
    </tbody>
  </table>
</div>
</template>


<script src="https://unpkg.com/lodash"></script>
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
        games: null,
        filteredProperty: 'name',
        activeFilters: [],
        query: null
    };
  },

  created: function() {
    axios
      .get('https://sheets.googleapis.com/v4/spreadsheets/1KlxXzRMWO3MdSEoQANpTuJOfFZ9iOiYtoPCxN9qc6CM/values/Sheet1?key=AIzaSyAOYzRf8SZJi4y7kaqYP8zSQ9orD1rJLyA')
      .then(res => {
        this.games = process(res.data);
      })
  },

  computed: { filtered() {
      var filtered = this.games
      this.activeFilters.forEach(filter => {
        filtered = filtered.filter(record => {
          return filter.name === 'name'
            ? new RegExp(filter.value, 'i').test(record[filter.name])
            : record[filter.name] == filter.value
        })
      })
      return filtered
    }
  },
  methods: { addFilter () {
      this.activeFilters.push({
        name: this.filteredProperty,
        value: this.query
      })
      this.query = ''
    },
    removeFilter (idx) {
      this.activeFilters.splice(idx, 1)
    }
  }
}

</script>

<style>
  h3 {
    margin-bottom: 5%;
  }
</style>
