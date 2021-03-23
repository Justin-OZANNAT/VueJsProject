<template>
  <div>
    <link
      rel="stylesheet"
      type="text/css"
      href="https://cdn.datatables.net/1.10.23/css/jquery.dataTables.min.css"
    />
    <link
      rel="stylesheet"
      type="text/css"
      href="https://cdn.datatables.net/buttons/1.6.5/css/buttons.dataTables.min.css"
    />
    <link
      rel="stylesheet"
      type="text/css"
      href="https://cdn.datatables.net/searchbuilder/1.0.1/css/searchBuilder.dataTables.min.css"
    />

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <a href="./assets/logo.png"></a>
      <img class="" src="../assets/logo.png" alt="salut" />
      <a class="navbar-brand" href="/"></a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarColor02"
        aria-controls="navbarColor02"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarColor02">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="/"
              >Accueil
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/Table">Données</a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input
            class="form-control mr-sm-2"
            type="text"
            placeholder="Search"
          />
          <button class="btn btn-secondary my-2 my-sm-0" type="submit">
            Search
          </button>
        </form>
      </div>
    </nav>
    <div class="container mt-5">
      <table id="tableau" class="display">
        <thead class="">
          <tr>
            <th>Name</th>
            <th>Id</th>
            <th>Gender</th>
            <th>Email</th>
            <th>Address</th>
            <th>Email</th>
            <th>Country</th>
            <th>Latitude</th>
            <th>Longitude</th>
            <th>Phone number</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="people in tableau" :key="people.id">
            <td>{{ people.firstname }}</td>
            <td>{{ people.lastname }}</td>
            <td>{{ people.gender }}</td>
            <td>{{ people.contact.email }}</td>
            <td>{{ people.contact.address }}</td>
            <td>{{ people.contact.city }}</td>
            <td>{{ people.contact.country }}</td>
            <td>{{ people.contact.location.lat }}</td>
            <td>{{ people.contact.location.lon }}</td>
            <td>{{ people.contact.phone }}</td>

          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>


<script>
import VueTableDynamic from 'vue-table-dynamic';
export default {
  name: "HelloWorld",
  data() {
    return {
        tableau: [],
    }
  },
  methods: {
    "sortTable": function sortTable(col) {
      this.rows.sort(function(a, b) {
        if (a[col] > b[col]) {
          return 1;
        } else if (a[col] < b[col]) {
          return  -1;
        }
        return 0;
      })
    },
    async getPeopleJson() {
      let url = "https://run.mocky.io/v3/70e5b0ad-7112-41c5-853e-b382a39e65b7";
      fetch(url)
        .then((dataJson) => dataJson.json())
        .then((data) => (this.tableau = data.people));
    }
  },
  computed: {
    "columns": function columns() {
      if (this.rows.length == 0) {
        return [];
      }
      return Object.keys(this.rows[0])
    },
  },
  created(){
    this.getPeopleJson();
  },
  components: { VueTableDynamic }
};
</script>

  

<style scoped>
table {
  font-family: 'Open Sans', sans-serif;
  width: 750px;
  border-collapse: collapse;
  border: 3px solid #44475C;
  margin: 10px 10px 0 10px;
}

table th {
  text-transform: uppercase;
  text-align: left;
  background: #44475C;
  color: #FFF;
  cursor: pointer;
  padding: 8px;
  min-width: 30px;
}
table th:hover {
        background: #717699;
      }
table td {
  text-align: left;
  padding: 8px;
  border-right: 2px solid #7D82A8;
}
table td:last-child {
  border-right: none;
}
table tbody tr:nth-child(2n) td {
  background: #D4D8F9;
}

table {
  background-color: lightgrey;
  color: black;
}

img:hover {
  box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
}
img {
  width: 2vw;
}
</style>
