<template>
  <div id="app">
    <div class="display">
      <h1>{{selected.toUpperCase()}}</h1>
      <table v-if="jsonSmgs">
        <tr v-for="(val, key, i) in jsonSmgs[selected]" :key="i">
          <td>{{key}}</td>
          <td>{{val}}</td>
        </tr>
      </table>
    </div>
    <div class="guns-wrap">
      <div class="guns">
        <ul v-for="(arr, cat, i) in guns" :key="i" :class="[`cat`, `cat--${cat}`]">
          <li :class="[`cat__li`, `cat__title`]">{{cat}}</li>
          <li v-for="(gun, i) in arr" :key="i" :class="[`cat__li`]">
            <p>{{gun}}</p>
          </li>
        </ul>
      </div>
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
      },
      selected: "r-99"
    };
  },
  methods: {
    async getJson(path) {
      const result = await fetch(path);
      const data = await result.json();
      return data;
    }
  },
  asyncComputed: {
    jsonSmgs() {
      return this.getJson(
        "https://cors-anywhere.herokuapp.com/https://raw.githubusercontent.com/BlackPelican/ApexLegendsWeaponStats/master/smgs.json"
      );
    }
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

:root {
  --color-a: #102542;
  --color-b: #f87060;
  --color-c: #cdd7d6;
}

html,
body,
#app {
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
  flex-direction: row;
}

.display {
  flex: 16;
  background: var(--color-c);
  height: 100%;
}

.guns-wrap {
  flex: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}

.guns {
  width: 60%;
  column-count: 2;
  column-gap: 4vmin;
}

.cat {
  list-style-type: none;
  margin-bottom: 4vmin;
  break-inside: avoid;
}

.cat__li {
  color: #333333ee;
  line-height: 4.2vmin;
  font-size: 2.6vmin;
}

.cat__li p {
  text-decoration: underline;
  cursor: pointer;
}

.cat__li p:hover {
  color: var(--color-b);
}

.cat__li.cat__title {
  color: var(--color-a);
  text-decoration: none;
  font-weight: 600;
  text-transform: uppercase;
}

table {
  border: 1px solid black;
}

td {
}
</style>
