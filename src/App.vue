<template>
  <div id="app">
    <input type="text" class="search" placeholder="Search gun..." />
    <div class="guns">
      <ul v-for="(arr, cat, i) in guns" :key="i" :class="[`cat`, `cat--${cat}`]">
        <li :class="[`cat__li`, `cat__title`]">{{cat}}</li>
        <li v-for="(gun, i) in arr" :key="i" :class="[`cat__li`]">{{gun}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => {
    return {
      guns: {
        ars: ["R-301", "Flatline", "Havoc", "L-Star", "G7 Scout", "Hemlok"],
        smgs: ["R-99", "Alternator", "Prowler"],
        lmgs: ["Spitfire", "Devotion"],
        snipers: [
          "Longbow",
          "Sentinel",
          "Kraber",
          "Charge Rifle",
          "Triple Take"
        ],
        shotguns: ["Peacekeeper", "Eva-8", "Mastiff"],
        pistols: ["P2020", "RE-45", "Wingman", "Mozambique"]
      }
    };
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Open+Sans:300,400,600,700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  position: relative;
  width: 100%;
  height: 100%;
  font-family: "Open Sans";
}

#app,
body {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.guns {
  margin-top: 12vmin;
  display: flex;
  flex-direction: row;
  background: pink;
  justify-content: space-between;
}

.cat {
  border: 1px solid black;
  list-style-type: none;
  margin-right: 4vmin;
}

.cat__title {
  font-weight: 600;
  text-transform: uppercase;
}

.cat__li {
  line-height: 4.2vmin;
  font-size: 2.6vmin;
}
</style>
