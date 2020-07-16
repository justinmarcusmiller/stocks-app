<template>
  <header id="header">
    <div id="header__Title">
      <h1>Stocks</h1>
    </div>
    <form id="header__SearchBar" @submit.prevent="search()">
      <input v-model="term" id="SearchBar__Box" type="text" />
      <button id="SearchBar__Button">Search</button>
    </form>
  </header>
</template>

<script>
export default {
  data() {
    return {
      term: null
    };
  },
  methods: {
    search: function() {
      //console.log(this.term)
      fetch(
        //"https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=IBM&apikey=demo"
        "https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=" + (this.term.toUpperCase()) + "&apikey=PTXOVNYY2ZY803KN"
      )
        .then(function(u) {
          return u.json();
        })
        .then((json) => {
          //console.log(json);
          if (json["Error Message"]) {
            console.log(json["Error Message"])
            this.$emit("updatejsondata", "error");
          } else {
            this.$emit("updatejsondata", json);
          }
        });
    },
  },
};
</script>

<style>
#header {
  background-color: #a17aff;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 165px;
}

#header__Title {
  margin-left: 75px;
}

#header__SearchBar {
  height: 53px;
  width: 373px;
  margin-right: 75px;
}

#SearchBar__Box {
  height: 53px;
  width: 287px;
  font-size: 21px;
  border: 1px solid #707070;
  border-right: 0;
  padding: 5px;
  transition: all 0.2s ease-in-out;
}

#SearchBar__Box:hover {
  background-color: rgba(255, 255, 255, 0.8);
}

#SearchBar__Button {
  height: 53px;
  width: 86px;
  font-size: 21px;
  border: 1px solid #707070;
  transition: all 0.2s ease-in-out;
}

#SearchBar__Button:hover {
  background-color: rgba(255, 255, 255, 0.6);
  cursor: pointer;
}
</style>
