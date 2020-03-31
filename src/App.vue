<template>
  <div id="app">
    <div class="wrap wrap--stats" :class="{'bg--dark':darkmode}">
      <h1 v-if="jsonGuns" class="title title--display">{{selected.toUpperCase()}}</h1>
      <table class="display__table" v-if="jsonGuns">
        <tr v-for="(val, key, i) in jsonGuns[selected]" :key="i">
          <td class="table__data table__data--key">{{key}}</td>
          <td class="table__data table__data--val">{{val}}</td>
        </tr>
      </table>
      <h1 class="title title--display" v-else>Fetching data...</h1>
    </div>
    <div class="wrap wrap--guns" :class="{'bg--darker':darkmode}">
      <div class="guns">
        <ul v-for="(arr, cat, i) in guns" :key="i" :class="[`cat`, `cat--${cat}`]">
          <li :class="[`title`, `title--cat`]">{{cat}}</li>
          <li v-for="(gun, i) in arr" :key="i" :class="{'cat__li':true}">
            <p @mouseover="setSelected(gun.toLowerCase())">{{gun}}</p>
          </li>
        </ul>
      </div>
      <img
        v-if="!darkmode"
        @mouseover="toggleDarkmode()"
        class="bulb"
        src="./assets/light.svg"
        alt="light"
      />
      <img v-else @mouseover="toggleDarkmode" class="bulb" src="./assets/dark.svg" alt="light" />
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
      selected: "r-99",
      darkmode: false
    };
  },
  methods: {
    async getJson(path) {
      const result = await fetch(path);
      const data = await result.json();
      return data;
    },
    setSelected(selected) {
      this.selected = selected;
    },
    toggleDarkmode() {
      this.darkmode = !this.darkmode;
    }
  },
  asyncComputed: {
    jsonGuns() {
      return this.getJson(
        "https://cors-anywhere.herokuapp.com/https://raw.githubusercontent.com/BlackPelican/apexInfo/dev/guns.json"
      );
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto:300,400,600,700&display=swap");
@import url("https://fonts.googleapis.com/css?family=Roboto+Slab:300,400,600,700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --color-white: #fff;
  --color-whitish: #e8e9eb;
  --color-black: #313638;
  --color-blackish: #313638ee;
  --color-accent: #d33f49;
}

html,
body,
#app {
  position: relative;
  height: 100%;
  width: 100%;
  font-family: "Roboto";
}

#app,
body {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: row;
}

.title {
  text-transform: uppercase;
  font-weight: 600;
  font-family: "Roboto Slab";
  color: var(--color-black);
  letter-spacing: 0.2vmin;
}

.wrap {
  height: 100%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  flex-direction: column;
  padding-bottom: 10vmin;
}

.wrap--stats {
  background: var(--color-white);
  flex: 16;
}

.wrap--guns {
  background: var(--color-whitish);
  flex: 10;
}

.title--display {
  margin-bottom: 4vmin;
}

.table__data {
  font-size: 2.6vmin;
  line-height: 4.2vmin;
}

.table__data--key {
  min-width: 30vmin;
  color: var(--color-blackish);
}

.table__data--val {
  font-weight: 600;
  color: var(--color-black);
  min-width: 15vmin;
}

.guns {
  column-count: 2;
}

.guns,
.display__table {
  min-width: 40vmin;
}

.cat {
  list-style-type: none;
  break-inside: avoid;
}

.cat:not(:last-child) {
  margin-bottom: 4vmin;
}

.cat__li,
.title--cat {
  line-height: 4.2vmin;
  font-size: 2.6vmin;
}

.cat__li p {
  color: var(--color-blackish);
  text-decoration: underline;
  cursor: pointer;
  letter-spacing: 0.1vmin;
}

.cat__li p:hover {
  color: var(--color-accent);
}

.bulb {
  height: 6vmin;
  position: absolute;
  top: 2vmin;
  right: 2vmin;
  cursor: pointer;
}

@media screen and (max-width: 1024px) {
  html,
  body,
  #app {
    height: auto;
  }

  #app {
    flex-direction: column;
  }

  .wrap {
    padding: 10vmax 0;
    justify-content: center;
  }

  .wrap--guns,
  .wrap--stats {
    width: 100%;
    flex: 1;
  }

  .guns,
  .display__table {
    min-width: 60vmin;
  }

  .title--display {
    font-size: 4.8vmin;
  }

  .cat__li,
  .title--cat,
  .table__data {
    font-size: 3vmin;
    line-height: 4.8vmin;
  }

  .table__data--val {
    min-width: 20vmin;
  }
}

@media screen and (max-width: 576px) {
  .cat__li,
  .title--cat,
  .table__data {
    font-size: 4vmin;
    line-height: 6.47vmin;
  }

  .title--display {
    font-size: 6.47vmin;
  }

  .table__data--val {
    min-width: 22vmin;
  }
}

.bg--darker {
  background: #2d3047;
}

.bg--darker .cat__li p,
.bg--dark .table__data--key {
  color: #ced0ed;
}

.bg--darker .cat__li p:hover {
  color: #d0a616;
}

.bg--dark {
  background: #444655;
}

.bg--dark .title,
.bg--dark .table__data--val,
.bg--darker .title--cat {
  color: #eceeff;
}
</style>
