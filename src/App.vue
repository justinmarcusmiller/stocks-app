<template>
  <div id="app">
    <Header @updatejsondata="updatejsondata($event)" />

    <p class="noDataError" v-if="apiData === null">
      Search for a stock by using the search-bar
    </p>
    <p class="noDataError" v-else-if="apiData === 'Error'">
      API Error, Please Enter A Different Search Term, Or Try Again Later.
    </p>
    <DataView
      v-else
      :symbol="symbol"
      :date="date"
      :open="open"
      :close="close"
      :high="high"
      :low="low"
      :volume="volume"
      :date1="date1"
      :date2="date2"
      :date3="date3"
      :date4="date4"
      :date5="date5"
      :date1close="date1_close"
      :date2close="date2_close"
      :date3close="date3_close"
      :date4close="date4_close"
      :date5close="date5_close"
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
      date1: null,
      date2: null,
      date3: null,
      date4: null,
      date5: null,
      date1_close: null,
      date2_close: null,
      date3_close: null,
      date4_close: null,
      date5_close: null,
    };
  },
  components: {
    Header,
    DataView,
  },
  methods: {
    convertDate(date, method) {
      if (method === 1) {
        return (
          date.getUTCMonth() +
          1 +
          "/" +
          date.getUTCDate() +
          "/" +
          (date.getYear() - 100)
        );
      } else {
        return (
          (date.getFullYear() + "-" + "0" + (date.getUTCMonth() + 1)) + "-" + date.getUTCDate()
        );
      }
    },
    updatejsondata(e) {
      const oneDay = 86400000;
      if (e !== "error") {
        const date1 = new Date(e["Meta Data"]["3. Last Refreshed"]);
        const date2 = new Date(date1 - oneDay);
        const date3 = new Date(date2 - oneDay);
        const date4 = new Date(date3 - oneDay);
        const date5 = new Date(date4 - oneDay);
        this.apiData = e;
        this.symbol = e["Meta Data"]["2. Symbol"];
        this.date = this.convertDate(date1, 1);
        this.date1 = this.convertDate(date1, 2);
        this.date2 = this.convertDate(date2, 2);
        this.date3 = this.convertDate(date3, 2);
        this.date4 = this.convertDate(date4, 2);
        this.date5 = this.convertDate(date5, 2);
        console.log(this.apiData);
        //console.log(this.apiData["Time Series (Daily)"][this.date2.toString()]["4. close"])
        this.date1_close = Number(this.apiData["Time Series (Daily)"][this.date1.toString()]["4. close"]).toFixed(2)
        this.date2_close = Number(this.apiData["Time Series (Daily)"][this.date2.toString()]["4. close"]).toFixed(2)
        this.date3_close = Number(this.apiData["Time Series (Daily)"][this.date3.toString()]["4. close"]).toFixed(2)
        this.date4_close = Number(this.apiData["Time Series (Daily)"][this.date4.toString()]["4. close"]).toFixed(2)  
        this.date5_close = Number(this.apiData["Time Series (Daily)"][this.date5.toString()]["4. close"]).toFixed(2)
        console.log(this.date5.toString())
        // date6 and date7 close are not working
        console.log(this.date3_close)
        console.log(this.date4_close)
        console.log(this.date5_close)

        //console.log(this.apiData["Time Series (Daily)"]["2020-02-26"]["1. open"])
        
        //console.log('"' + this.date2.toString() + '"')
        //this.date1_close = this.apiData["Time Series (Daily)"];
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
        this.apiData = "Error";
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
