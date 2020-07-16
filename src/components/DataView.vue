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
    <!-- <Graph /> -->
    
  </div>
</template>

<script>
//import Graph from "@/components/Graph.vue";


export default {
  props: ["symbol", "date", "open", "close", "high", "low", "volume"],
  data() {
    return {
    };
  },
  components: {
    //Graph
  },
}
</script>

<style>
#dataView {
  color: #707070;
  display: grid;
  grid-template-columns: 620px 1fr;
  grid-template-rows: 171px 1fr;
  justify-items: center;
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

</style>
