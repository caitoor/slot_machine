<template>
  <div class="configs">
    <table>
      <thead></thead>
      <tbody>
        <tr>
          <td>
            <label for="slots">Anzahl Slots</label>
          </td>
          <td>
            <input
              type="number"
              id="slots"
              name="slots"
              min="2"
              max="100"
              v-model="slots"
            />
          </td>
        </tr>
        <tr>
          <td>Beginn Besprechung</td>
          <td>
            <input
              type="number"
              id="start-h"
              name="end"
              min="8"
              max="20"
              v-model="startH"
            />:
            <input
              type="number"
              id="start-m"
              name="end"
              min="0"
              max="55"
              step="5"
              v-model="startM"
            />
            Uhr
          </td>
        </tr>
        <tr>
          <td>Ende Besprechung</td>
          <td>
            <input
              type="number"
              id="end-h"
              name="end"
              min="8"
              max="20"
              v-model="endH"
            />:
            <input
              type="number"
              id="end-m"
              name="end"
              min="0"
              max="55"
              step="5"
              v-model="endM"
            />
            Uhr
          </td>
        </tr>
        <tr>
          <td><label for="breaks">Anzahl Pausen</label></td>
          <td>
            <input
              type="number"
              id="breaks"
              name="breaks"
              min="0"
              max="5"
              v-model="breakCount"
            />
          </td>
        </tr>
        <tr>
          <td><label for="break-duration">Dauer Pausen</label></td>
          <td>
            <input
              type="number"
              id="break-duration"
              name="break-duration"
              min="1"
              max="120"
              v-model="breakDuration"
            />
            Min
          </td>
        </tr>
        <tr>
          <td><label for="puffer">Slotpuffer</label></td>
          <td>
            <input
              type="number"
              id="puffer"
              name="puffer"
              min="0"
              max="10"
              v-model="puffer"
            />
            Min
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "ConfigBar",
  props: {},
  data: function () {
    return {
      startH: 9,
      startM: 0,
      endH: 11,
      endM: 15,
      slots: 10,
      start: new Date(0, 0, 1, 9, 0),
      end: new Date(0, 0, 1, 11, 15),
      breakCount: 1,
      breakDuration: 10,
      puffer: 2,
    };
  },
  computed: {
    settings: function () {
      return {
        start: new Date(0, 0, 1, this.startH, this.startM),
        end: new Date(0, 0, 1, this.endH, this.endM),
        slots: this.slots,
        breakCount: this.breakCount,
        breakDuration: this.breakDuration,
        puffer: this.puffer,
      };
    },
  },
  methods: {},
  mounted: function () {},
  updated: function () {
    this.$emit('settingsChanged', this.settings);
  },
};
</script>