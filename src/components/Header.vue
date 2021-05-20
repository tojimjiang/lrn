<template>
  <div id="header">
    <label for="number-range">Number Range</label>
    <input type="text" id="number-range" v-model="rangeString" />
    <span v-if="numberRangeError" class="error"
      >Number range provided is not valid</span
    >
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    range: Array,
    op: Number,
  },
  data: function () {
    return {
      rangeString: `${this.range[0]}-${this.range[1]}`,
      numberRangeError: false,
    };
  },
  watch: {
    rangeString: function (val) {
      let rangeArr = val.split("-");
      const pattern = /^[0-9]{1,2}-[0-9]{1,2}$/;
      // console.log(val.match(pattern));
      if (rangeArr.length == 2 && val.match(pattern)) {
        // console.log(parseInt(rangeArr[0]), parseInt(rangeArr[1]));
        if (
          rangeArr[0] &&
          !Number.isNaN(
            parseInt(rangeArr[0]) &&
              rangeArr[1] &&
              !Number.isNaN(parseInt(rangeArr[1]))
          )
        ) {
          this.numberRangeError = false;
          this.$emit("newRange", {newRange: rangeArr.map((elt) => {return parseInt(elt)})});
        } else {
          this.numberRangeError = true;
        }
      } else {
        this.numberRangeError = true;
      }
    },
  },
  methods: {
  }
};
</script>