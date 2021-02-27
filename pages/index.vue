<template>
  <v-row justify="center" align="center">
    <v-col cols="10" sm="12" md="12">
      <header class="api-title">
        <h1 style="width: 100%">Proxim API</h1>
        <h2>Overview</h2>
      </header>
      <main>
        <div class="statuses-overview">
          <h3>Endpoint Statuses</h3>
          <ol>
            <li v-for="(status, i) in statuses" :key="i">
              {{ status.text }}
            </li>
          </ol>
        </div>
        <hr />
        <ul class="endpoint-sets-list">
          <li v-for="(set, k) in endpointsList" :key="k" class="endpoint-set">
            <h2 class="set-name" @click="toggleSet(set)">
              {{ set.setName }}
            </h2>
            <ul
              v-show="set.expand"
              class="endpoints-list animate__animated"
              :class="{
                animate__fadeIn: !set.setExpand,
                animate__fadeOut: set.setExpand,
              }"
            >
              <li
                v-for="(endpoint, j) in set.endpoints"
                :key="j"
                class="endpoint"
              >
                <div class="method">{{ endpoint.method }}</div>
                <div class="url">{{ endpoint.url }}</div>
                <div class="status" :class="getStatusClass(endpoint.status)">
                  {{ getStatusText(endpoint.status) }}
                </div>
                <div class="notes">
                  <span>{{ endpoint.notes }}</span>
                </div>
              </li>
            </ul>
          </li>
        </ul>
      </main>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      statuses: [
        // {
        //   name: '<status name>',
        //   text: 'Mock',
        //   order: 0,
        // },
      ],
      endpointsList: [
        // {
        //   setName: '<set name>',
        //   expand: true,
        //   endpoints: [
        //     {
        //       method: '<method>',
        //       url: 'url name',
        //       status: <status code>,
        //     }
        //   ],
        // },
      ],
    }
  },
  computed: {},
  methods: {
    isExpanded(set) {
      return set.expand
    },
    toggleSet(set) {
      set.expand = !set.expand
    },
    getStatusClass(status) {
      return status >= 0 && status < this.statuses.length
        ? this.statuses[status].name
        : '---'
    },
    getStatusText(status) {
      return status >= 0 && status < this.statuses.length
        ? this.statuses[status].text
        : '---'
    },
  },
}
</script>

<style>
html {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
header.api-title {
  background-color: #f1f1f1;
  padding: 20px;
  text-align: center;
}
main {
  padding: 20px;
}
ul.endpoint-sets-list {
  list-style-type: none;
  margin: 0 auto;
  padding: 0;
  width: 100%;
  min-width: 400px;
}
ul.endpoints-list {
  margin-left: 0;
  padding-left: 0;
  margin-bottom: 15px;
  list-style-type: none;
}
.endpoint-set {
  padding: 20px;
}
.endpoint {
  background-color: #f1f1f1;
  margin-bottom: 5px;
  padding: 20px;
  display: flex;
  flex-direction: row;
}
.endpoint .method {
  flex: 0 0 80px;
  padding: 5px;
  margin-right: 5px;
}
.endpoint .url {
  padding: 5px;
  flex: 1 1 auto;
  min-width: 400px;
}
.endpoint .status {
  padding: 5px;
  margin-left: 5px;
  flex: 0 0 shrink;
  font-weight: bold;
  border-radius: 5px;
}

.endpoint .notes {
}

.status.mock {
  background-color: brown;
  color: white;
}

.status.port {
  background-color: black;
  color: white;
}
.status.backend-test {
  background-color: darkblue;
  color: white;
}
.status.console-test {
  background-color: darkorange;
  color: white;
}
.status.stable {
  background-color: darkgreen;
  color: white;
}
.set-name {
  width: 100%;
  text-align: center;
  color: grey;
  cursor: pointer;
}
.badge {
  width: 50px;
  color: white;
  text-align: center;
}
.statuses-overview {
  width: 20%;
  /* min-width: 200px; */
  margin: 0 auto;
  margin-bottom: 10px;
}
</style>
