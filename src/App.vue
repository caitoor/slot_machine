<template>
  <div id="wrapper">
    <header>
      <h1>Besprechungsslots</h1>
    </header>

    <main>
      <ConfigBar @settingsChanged="onSettingsChange" />
      <SlotTable v-bind:settings="settings" />
    </main>
  </div>
</template>

<script>
import ConfigBar from "./components/ConfigBar.vue";
import SlotTable from "./components/SlotTable.vue";

export default {
  name: "App",
  components: {
    ConfigBar,
    SlotTable,
  },
  data: function () {
    return {
      settings: {
        slots: 10,
        start: new Date(0, 0, 1, 9, 0),
        end: new Date(0, 0, 1, 11, 15),
        breakCount: 1,
        breakDuration: 10,
        puffer: 2,
      },
    };
  },
  methods: {
    onSettingsChange: function (newSettings) {
      for (let val in newSettings) {
        this.settings[val] = newSettings[val];
      }
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  background-color: #222;
  color: white;
  font-family: "Fira Sans", monospace;
  margin: 0;
}

#wrapper {
  width: 500px;
  margin: auto;
  overflow: hidden;
}

a,
a:hover,
a:visited {
  color: white;
}

input {
  width: 50px;
}

.slots {
  padding-top: 20px;
}

.slots td {
  padding: 1px 5px;
}

.slots tr:nth-child(odd) {
  background-color: #333;
}

.invisible {
  display: none;
}

button {
  background-color: #222;
  color: white;
  cursor: pointer;
  border: 1px solid white;
  margin-top: 10px;
}

button:hover {
  background-color: #333;
}
</style>
