<template>
  <div class="slots">
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>from</th>
          <th>until</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="slot in slots" :key="slot.id">
          <td>{{ slot.id }}</td>
          <td>{{ slot.from }}</td>
          <td>{{ slot.until }}</td>
        </tr>
      </tbody>
    </table>
    <button v-on:click="copyTable">Copy</button>
  </div>
</template>

<script>
export default {
  name: "SlotTable",
  props: { settings: Object },
  data: function () {
    return {
      config: this.settings,
    };
  },
  computed: {
    slots: function () {
      let s = [];
      const values = { ...this.config };

      const duration = Math.abs(
        Date.parse(values.start) - Date.parse(values.end)
      );
      const downTime =
        values.puffer * (values.slots - 1 - values.breakCount) +
        values.breakCount * values.breakDuration;

      const slotTime = Math.floor((duration - downTime * 60000) / values.slots);
      const slotsUntilBreak = values.slots / (parseInt(values.breakCount) + 1);

      for (let i = 0; i < values.slots; i++) {
        let slot = {};
        slot.id = i + 1;
        const passedBreaks = Math.floor(i / slotsUntilBreak);
        const passedBreakTime = passedBreaks * values.breakDuration * 60000;
        const passedPufferTime = (i - passedBreaks) * values.puffer * 60000;
        const passedSlotTime = i * slotTime;
        let startTime =
          Date.parse(values.start) +
          passedSlotTime +
          passedPufferTime +
          passedBreakTime;
        let endTime = new Date(startTime + slotTime);
        startTime = new Date(startTime);
        slot.from =
          startTime.getHours() +
          ":" +
          startTime.getMinutes().toString().padStart(2, "0") +
          ":" +
          startTime.getSeconds().toString().padStart(2, "0");
        slot.until =
          endTime.getHours() +
          ":" +
          endTime.getMinutes().toString().padStart(2, "0") +
          ":" +
          endTime.getSeconds().toString().padStart(2, "0");
        s.push(slot);
      }
      return s;
    },
  },
  methods: {
    copyTable: function () {
      let outputText = "";
      this.slots.forEach((slot) => {
        outputText += slot.id + "\t" + slot.from + "\t" + slot.until + "\n";
      });
      $(".slots").append(
        $('<textarea id="copytext">' + outputText + "</textarea>")
      );
      let copyText = document.getElementById("copytext");
      copyText.select();
      copyText.setSelectionRange(0, 99999);
      document.execCommand("copy");
      $("#copytext").remove();
    },
  },
};
</script>

<style scoped>
</style>
