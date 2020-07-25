<template>
  <div id="dataView">
    <div id="dataView__Header">
      <h2>{{ symbol }}</h2>
    </div>
    <div id="dataView__Data">
      <p id="date" class="dataDisplay">{{ date }}</p>
      <div id="openData" class="dataDisplay">
        <p class="data__type">Open</p>
        <p class="data__num">{{ open }}</p>
      </div>
      <div id="closeData" class="dataDisplay">
        <p class="data__type">Close</p>
        <p class="data__num">{{ close }}</p>
      </div>
      <div id="highData" class="dataDisplay">
        <p class="data__type">High</p>
        <p class="data__num">{{ high }}</p>
      </div>
      <div id="lowData" class="dataDisplay">
        <p class="data__type">Low</p>
        <p class="data__num">{{ low }}</p>
      </div>
      <div id="volumeData" class="dataDisplay">
        <p class="data__type">Volume</p>
        <p class="data__num">{{ volume }}</p>
      </div>
    </div>
    <div id="graph">
      <la-cartesian
        :autoresize="true"
        :bound="[(n) => (n - 1).toFixed(0), (n) => (n + 1).toFixed(0)]"
        textColor="#707070"
        :data="[
          { name: 'open', pv: open },
          { name: 'low', pv: low },
          { name: 'high', pv: high },
          { name: 'close', pv: close },
        ]"
      >
        <la-line dot curve prop="pv"></la-line>
        <la-x-axis prop="name" gridline></la-x-axis>
        <la-y-axis gridline></la-y-axis>
        <la-tooltip></la-tooltip>
      </la-cartesian>
    </div>
  </div>
</template>

<script>
import { Laue } from "laue";
import { Cartesian, Line, XAxis, YAxis, Tooltip } from "laue";

export default {
  props: [
    "symbol",
    "date",
    "open",
    "close",
    "high",
    "low",
    "volume",
    "date1",
    "date1close",
  ],
  components: {
    LaCartesian: Cartesian,
    LaLine: Line,
    laTooltip: Tooltip,
    laXAxis: XAxis,
    laYAxis: YAxis,
  },
  data() {
    return {
      show: "line",
    };
  },
};
</script>

<style>
#dataView {
  color: #707070;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 171px 1fr;
  justify-items: center;
  padding-right: 25px;
  padding-left: 25px;
  padding-bottom: 25px;
}

#dataView__Header {
  grid-column: 1 / 3;
  height: 171px;
}

#dataView__Header h2 {
  font-size: 61px;
  font-weight: 400;
}

#dataView__Data {
  font-size: 37px;
  text-align: center;
}

#date {
  justify-content: center;
  width: 175px;
  margin: auto;
  margin-bottom: 75px;
}

.dataDisplay {
  border-bottom: 1px solid #707070;
  text-align: center;
  display: flex;
  width: 396px;
  justify-content: space-between;
  margin-bottom: 30px;
}

#graph {
  display: flex;
  align-items: center;
  padding: 25px;
  border: 1px solid #707070;
}

@media only screen and (max-width: 1200px) {
  #dataView {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 25px 0;
  }

  #dataView__Header {
    height: 100px;
  }

  #date {
    margin-bottom: 25px;
  }

  .dataDisplay {
    max-width: 75vw;
  }

  #dataView__Data {
    font-size: 24px;
  }

  #graph {
  }
}

@media only screen and (max-width: 400px) {
}
</style>
