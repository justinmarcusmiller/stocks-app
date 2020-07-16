<template>
  <div id="app">
    <Header @updatejsondata="updatejsondata($event)" />
    
    <p class="noDataError" v-if="apiData === null">
      Search for a stock using the search-bar
    </p>
    <p class="noDataError" v-else-if="apiData === 'Error'">API Error, Please Enter A Different Search Term, Or Try Again Later.</p>
    <DataView
      v-else
      :symbol="symbol"
      :date="date"
      :open="open"
      :close="close"
      :high="high"
      :low="low"
      :volume="volume"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import DataView from "./components/DataView.vue";

export default {
  name: "App",
  data() {
    return {
      apikey: "PTXOVNYY2ZY803KN",
      apiData: null,
      symbol: null,
      date: null,
      open: null,
      close: null,
      high: null,
      low: null,
      volume: null,
    };
  },
  components: {
    Header,
    DataView,
  },
  methods: {
    updatejsondata(e) {
      if (e !== "error") {
        const date1 = new Date(e["Meta Data"]["3. Last Refreshed"]);
        this.apiData = e;
        this.symbol = e["Meta Data"]["2. Symbol"];
        //console.log(date1);
        this.date =
          date1.getUTCMonth() +
          1 +
          "/" +
          date1.getUTCDate() +
          "/" +
          (date1.getYear() - 100);
        this.open = Number(
          e["Time Series (Daily)"][e["Meta Data"]["3. Last Refreshed"]][
            "1. open"
          ]
        ).toFixed(2);
        this.close = Number(
          e["Time Series (Daily)"][e["Meta Data"]["3. Last Refreshed"]][
            "4. close"
          ]
        ).toFixed(2);
        this.high = Number(
          e["Time Series (Daily)"][e["Meta Data"]["3. Last Refreshed"]][
            "2. high"
          ]
        ).toFixed(2);
        this.low = Number(
          e["Time Series (Daily)"][e["Meta Data"]["3. Last Refreshed"]][
            "3. low"
          ]
        ).toFixed(2);
        this.volume = e["Time Series (Daily)"][
          e["Meta Data"]["3. Last Refreshed"]
        ]["5. volume"]
          .toString()
          .replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1,");
      } else {
        this.apiData = "Error"
      }
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  color: #707070;
}

.noDataError {
  font-size: 37px;
  text-align: center;
  margin-top: 75px;
  opacity: 0.8;
}

h1 {
  font-size: 69px;
  color: #ffffff;
  font-weight: 400;
}
</style>
